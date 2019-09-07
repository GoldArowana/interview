# synchronized关键字

## synchronized概念
oracle官方解释：https://docs.oracle.com/javase/tutorial/essential/concurrency/syncmeth.html
>Synchronized methods enable a simple strategy for preventing thread interference and memory consistency errors: if an object is visible to more than one thread, all reads or writes to that object's variables are done through synchronized methods.

上面这段翻译后就是：
>同步方法支持一种简单的策略来防止线程干扰和内存一直想错误：如果一个对象对多个线程可见，则该对象变量的所有读取和写入都是通过同步方法完成的。

总之，synchronized关键词是为了解决线程安全问题而出现的。

## 线程不安全的例子
```java
public class ThreadUnsafeWithoutSynchronized1 {
    private static final int THOUSAND = 1000;
    private static int counter = 0;

    private static Runnable runnable = () -> {
        for (int i = 0; i < 10 * THOUSAND; i++) {
            counter++;
        }
    };

    public static void main(String[] args) throws InterruptedException {
        // 实例化两个线程
        Thread t1 = new Thread(runnable);
        Thread t2 = new Thread(runnable);

        // 运行这两个线程
        t1.start();
        t2.start();

        // 让主线程等待t1和t2执行完。
        t1.join();
        t2.join();

        // t1和t2执行完后，打印counter的最终结果。
        System.out.println(counter);
    }
}
```

## synchronized的五种用法
### 一、 代码块+自定义锁对象
```java
/**
 * synchronized关键词的第一种用法示例：自定义锁对象 + 代码块形式。
 * 用synchronized修饰后，两个线程不会交替执行；在没有synchronized修饰时，则可能会交替执行。
 *
 * @author arowana
 */
public class SynchronizedObjectCodeBlock {
    private static final Object LOCK = new Object();

    private static Runnable runnable = () -> {
        synchronized (LOCK) {
            for (int i = 0; i < 10; i++) {
                try {
                    System.out.println("当前执行的线程是：" + Thread.currentThread().getName());
                    TimeUnit.SECONDS.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    };

    public static void main(String[] args) {
        // 实例化两个线程
        Thread t1 = new Thread(runnable);
        Thread t2 = new Thread(runnable);

        // 运行这两个线程
        t1.start();
        t2.start();
    }
}
```
### 二、 代码块+this对象锁
```java
/**
 * synchronized关键词的第二种用法示例：代码块形式 + this对象锁
 * 用synchronized修饰后，两个线程不会交替执行；在没有synchronized修饰时，则可能会交替执行。
 *
 * @author arowana
 */
public class SynchronizedThisCodeBlock implements Runnable {
    @Override
    public void run() {
        synchronized (this) {
            for (int i = 0; i < 10; i++) {
                try {
                    System.out.println("当前执行的线程是：" + Thread.currentThread().getName());
                    TimeUnit.SECONDS.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    public static void main(String[] args) {
        SynchronizedThisCodeBlock instance = new SynchronizedThisCodeBlock();

        // 实例化两个线程
        Thread t1 = new Thread(instance);
        Thread t2 = new Thread(instance);

        // 运行这两个线程
        t1.start();
        t2.start();
    }
}
```
### 三、 代码块+Class对象
```java
/**
 * synchronized关键词的第二种用法示例：类对象锁 + 代码块形式。
 * 用synchronized修饰后，两个线程不会交替执行；在没有synchronized修饰时，则可能会交替执行。
 *
 * @author arowana
 */
public class SynchronizedClassCodeBlock {
    private static Runnable runnable = () -> {
        synchronized (SynchronizedClassCodeBlock.class) {
            for (int i = 0; i < 10; i++) {
                try {
                    System.out.println("当前执行的线程是：" + Thread.currentThread().getName());
                    TimeUnit.SECONDS.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    };

    public static void main(String[] args) {
        // 实例化两个线程
        Thread t1 = new Thread(runnable);
        Thread t2 = new Thread(runnable);

        // 运行这两个线程
        t1.start();
        t2.start();
    }
}
```
### 四、 修饰普通成员方法
```java
/**
 * synchronized关键词的第四种用法：在普通成员方法前面修饰synchronized关键词。
 * 这种用法等价于第二种用法{@link SynchronizedThisCodeBlock}
 * 用synchronized修饰后，两个线程不会交替执行；在没有synchronized修饰时，则可能会交替执行。
 *
 * @author arowana
 */
public class SynchronizedMethod implements Runnable {
    @Override
    public void run() {
        innerSyncMethod();
    }

    private synchronized void innerSyncMethod() {
        for (int i = 0; i < 10; i++) {
            try {
                System.out.println("当前执行的线程是：" + Thread.currentThread().getName());
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        SynchronizedThisCodeBlock instance = new SynchronizedThisCodeBlock();

        // 实例化两个线程
        Thread t1 = new Thread(instance);
        Thread t2 = new Thread(instance);

        // 运行这两个线程
        t1.start();
        t2.start();
    }
}
```

### 五、 修饰静态方法
```java
/**
 * synchronized关键词的第五种用法：在静态方法前面修饰synchronized关键词。
 * 这种用法等价于第三种用法{@link SynchronizedClassCodeBlock}
 * 用synchronized修饰后，两个线程不会交替执行；在没有synchronized修饰时，则可能会交替执行。
 *
 * @author arowana
 */
public class SynchronizedStaticMethod {

    private synchronized static void innerSyncMethod() {
        for (int i = 0; i < 10; i++) {
            try {
                System.out.println("当前执行的线程是：" + Thread.currentThread().getName());
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        Runnable runnable = SynchronizedStaticMethod::innerSyncMethod;

        // 实例化两个线程
        Thread t1 = new Thread(runnable);
        Thread t2 = new Thread(runnable);

        // 运行这两个线程
        t1.start();
        t2.start();
    }
}
```
## synchronized方法执行前后的状态
running -> blocked -> running

## 方法抛出异常后，会释放锁吗
会。正常结束代码块，或者是异常退出代码块，都会自动释放锁。

## 可重入
可重入指的是：同一线程的外层函数获得锁之后，内层函数可以直接再次获取该锁

可重入演示代码：
```java
/**
 * 演示synchronized的可重入性质
 * 在exe方法获取到this锁后，在内部嵌套的方法中，可以再次获取到this锁
 *
 * @author arowana
 */
public class SynchronizedReentrant {
    private synchronized void exe1() {
        System.out.println("1");
    }

    private synchronized void exe() {
        System.out.println("exe");
        exe1();
    }

    public static void main(String[] args) {
        SynchronizedReentrant instance = new SynchronizedReentrant();
        instance.exe();
    }
}
```

jvm会在每次获取锁(进入synchronized代码块)时让计数器+1，每次释放锁(退出synchronized代码块)时让技术器-1。计数器为0则表示释放状态。 

所以，可重入性质的原理就是：一个线程在第一次获取锁时，锁计数器会变为1；同一个线程再次获取锁时，只需让计数器变为2就可以了。

## 不可中断
相比于juc下的Lock，synchronized不会响应中断。

## monitor

## synchronized的缺点
1. 效率低：不能响应中断、不可手动释放、获取锁时不能设定超时时间
2. 相比于读写锁，synchronized不够灵活
3. 无法返回是否获取到锁的结果，只能一直等下去

## 使用synchronized的注意事项
1. 锁对象不能为空
2. 作用于不宜过大
3. 避免死锁

## 多个线程等待同一个synchronized锁时，jvm如何选择下一个获取锁的线程是哪个？
synchronized是非公平锁,无法保证等待的线程获取锁的顺序。

## 锁升级、降级
偏向所、轻量级锁、重量级锁