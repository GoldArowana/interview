# 停止线程

## 如何正确停止线程？
<p>使用interrupt来通知，而不是强制停止
<p>例如像下面这段代码这样直接调用stop停止线程是不优雅的：

```java
/**
 * 错误的停止方法：用stop()来停止线程，会导致线程运行一半突然停止，
 * 没办法完成一个基本单位的操作（一个连队），会造成脏数据（有的连队少领取装备）。
 */
public class StopThread {

    private static Runnable runnable = () -> {
        //模拟指挥军队：一共有5个连队，每个连队10人，以连队为单位，发放武器弹药，叫到号的士兵前去领取
        for (int i = 0; i < 5; i++) {
            System.out.println("连队" + i + "开始领取武器");
            for (int j = 0; j < 10; j++) {
                System.out.println(j);
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("连队" + i + "已经领取完毕");
        }
    };

    public static void main(String[] args) {
        Thread thread = new Thread(runnable);
        thread.start();
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        thread.stop();
    }
}

```

## 正确停止线程的方式

### case1: run方法内没有sleep或wait方法时，停止线程

```java
public class RightWayStopThreadWithoutSleep {
    private static Runnable runnable = () -> {
        for (int i = 0; !Thread.currentThread().isInterrupted() && i < 1000000; i++) {
            System.out.println(i);
        }
    };

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();

        TimeUnit.SECONDS.sleep(1);
        thread.interrupt();
    }
}
```

### case2: 带有sleep的中断线程的写法

```java
public class RightWayStopThreadWithSleep {

    private static Runnable runnable = () -> {
        for (int i = 0; !Thread.currentThread().isInterrupted() && i < 1000000; i++) {
            System.out.println(i);
        }

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            System.out.println("在sleep时被中断");
        }

    };

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(500);
        thread.interrupt();
    }
}
```

### case3: sleep方法出现在循环中时
<p>如果把响应中断的try catch放到循环里，就很容易出错。在指定到sleep时如果发生的中断，那么会catch住，并且中断标记会被清除。而且在进入到下一个循环时，仍可以继续执行，因为Thread.currentThread().isInterrupted()仍然为false
<p>下面这段代码就是错误的样例：

```java
public class WrongWayStopThreadWithSleepEveryLoop {
    private static Runnable runnable = () -> {
        for (int i = 0; !Thread.currentThread().isInterrupted() && i < 1000000; i++) {
            System.out.println(i);

            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                System.out.println("在sleep时被中断");
            }
        }
    };

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(5000);
        thread.interrupt();
    }
}
```
<p>如果在执行过程中，每次循环都会调用sleep或wait等方法，那么不需要每次迭代都检查是否已中断
<p>正确形式请参考下面这段代码：

```java
public class RightWayStopThreadWithSleepEveryLoop {
    private static Runnable runnable = () -> {
        try {
            for (int i = 0; !Thread.currentThread().isInterrupted() && i < 1000000; i++) {
                System.out.println(i);
                Thread.sleep(10);
            }
        } catch (InterruptedException e) {
            System.out.println("在sleep时被中断");
        }
    };

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(3000);
        thread.interrupt();
    }
}
```

### case4: 对于run方法内调用的函数
<p>对于run方法中嵌套调用的方法，1. 要么应该声明异常，2. 要么应该catch后恢复中断状态，来让上层感知到。
<p>声明异常例如下面代码中的throwInMethod()方法：

```java
public class RightWayStopThreadInProd {
    private static Runnable runnable = () -> {
        while (!Thread.currentThread().isInterrupted()) {
            System.out.println("go");
            try {
                throwInMethod();
            } catch (InterruptedException e) {
                //保存日志、停止程序
                System.out.println("保存日志");
                e.printStackTrace();
            }
        }
    };

    private static void throwInMethod() throws InterruptedException {
        Thread.sleep(2000);
    }

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(1000);
        thread.interrupt();
    }
}
```

<p>catch后恢复中断状态例如下面的reInterrupt()方法：

```java
public class RightWayStopThreadInProd2 {

    private static Runnable runnable = () -> {
        while (true) {
            if (Thread.currentThread().isInterrupted()) {
                System.out.println("Interrupted，程序运行结束");
                break;
            }
            reInterrupt();
        }
    };

    private static void reInterrupt() {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            e.printStackTrace();
        }
    }

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(1000);
        thread.interrupt();
    }
}
```

### case5: 用volatile停止线程
<p>使用volatile停止线程在一般场景下是可以的，如下面这个例子：

```java
public class WrongWayVolatile {
    private static volatile boolean canceled = false;
    private static Runnable runnable = () -> {
        int num = 0;
        try {
            while (num <= 100000 && !canceled) {
                if (num % 100 == 0) {
                    System.out.println(num + "是100的倍数。");
                }
                num++;
                Thread.sleep(1);
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    };

    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(5000);
        canceled = true;
    }
}
```

<p>但是在一些场景下volatile方式不能正常停止线程，代码如下：
（生产者会阻塞在storage.put(num)处，不会结束进程，volatile方式没有能力解除BlockingQueue中put方法的阻塞）

```java
/**
 * 演示用volatile的局限part2 陷入阻塞时，volatile是无法线程的
 * 此例中，生产者的生产速度很快，消费者消费速度慢，所以阻塞队列满了以后，生产者会阻塞，等待消费者进一步消费
 * <p>
 * 正确方式请参考{@link WrongWayVolatileFixed}
 *
 * @author arowana
 */
public class WrongWayVolatileCantStop {

    public static void main(String[] args) throws InterruptedException {
        ArrayBlockingQueue storage = new ArrayBlockingQueue(10);

        // 开辟新线程运行生产者，然后睡眠1秒
        Producer producer = new Producer(storage);
        Thread producerThread = new Thread(producer);
        producerThread.start();
        TimeUnit.SECONDS.sleep(1);

        // 创建消费者
        Consumer consumer = new Consumer(storage);
        // 若干次消费后，就会退出这个循环
        while (consumer.needMoreNums()) {
            System.out.println(consumer.storage.take() + "被消费了");
            Thread.sleep(100);
        }
        System.out.println("消费者不需要更多数据了。");

        // 一旦消费不需要更多数据了，我们应该让生产者也停下来，
        // 但是实际情况是生产者会阻塞在storage.put(num)处，不会结束进程
        producer.canceled = true;
        System.out.println(producer.canceled);
    }

    /**
     * 生产者
     */
    static class Producer implements Runnable {
        volatile boolean canceled = false;
        BlockingQueue storage;

        Producer(BlockingQueue storage) {
            this.storage = storage;
        }

        @Override
        public void run() {
            int num = 0;
            try {
                while (num <= 100000 && !canceled) {
                    if (num % 100 == 0) {
                        storage.put(num);
                        System.out.println(num + "是100的倍数,被放到仓库中了。");
                    }
                    num++;
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                System.out.println("生产者结束运行");
            }
        }
    }

    /**
     * 消费者
     */
    static class Consumer {
        BlockingQueue storage;

        Consumer(BlockingQueue storage) {
            this.storage = storage;
        }

        /**
         * 百分之5的概率会返回false
         */
        boolean needMoreNums() {
            return Math.random() < 0.95;
        }
    }
}
```

<p>针对于这种阻塞队列的情况，还是应该使用中断的方式来停止线程。
<p>对上述代码的错误进行修复，请参考下面这段代码：</p>

```java
/**
 * 用中断来修复{@link WrongWayVolatileCantStop}的无尽等待问题
 *
 * @author arowana
 */
public class WrongWayVolatileFixed {

    public static void main(String[] args) throws InterruptedException {
        ArrayBlockingQueue storage = new ArrayBlockingQueue(10);

        // 开辟新线程运行生产者，然后睡眠1秒
        Producer producer = new Producer(storage);
        Thread producerThread = new Thread(producer);
        producerThread.start();
        TimeUnit.SECONDS.sleep(1);

        // 创建消费者
        Consumer consumer = new Consumer(storage);
        // 若干次消费后，就会退出这个循环
        while (consumer.needMoreNums()) {
            System.out.println(consumer.storage.take() + "被消费了");
            Thread.sleep(100);
        }
        System.out.println("消费者不需要更多数据了。");

        producerThread.interrupt();
    }


    static class Producer implements Runnable {
        BlockingQueue storage;

        Producer(BlockingQueue storage) {
            this.storage = storage;
        }

        @Override
        public void run() {
            int num = 0;
            try {
                while (num <= 100000 && !Thread.currentThread().isInterrupted()) {
                    if (num % 100 == 0) {
                        storage.put(num);
                        System.out.println(num + "是100的倍数,被放到仓库中了。");
                    }
                    num++;
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                System.out.println("生产者结束运行");
            }
        }
    }

    static class Consumer {
        BlockingQueue storage;

        Consumer(BlockingQueue storage) {
            this.storage = storage;
        }

        /**
         * 百分之5的概率会返回false
         */
        boolean needMoreNums() {
            return Math.random() < 0.95;
        }
    }
}
```
