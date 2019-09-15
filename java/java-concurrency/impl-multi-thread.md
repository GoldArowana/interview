# 实现多线程

## 实现多线程有几种方法

Oracle官方的解释是两种:

### 第一种、继承Thread类

```java
public class MultiThreadWithExtends {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.start();
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println(this.getName() + " is running");
    }
}
```

### 第二种、实现Runnable接口

```java
public class MultiThreadByRunnable {
    public static void main(String[] args) {
        MyRunnable runnable = new MyRunnable();
        Thread thread = new Thread(runnable);
        thread.start();
    }
}

class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + " is running");
    }
}

```

### 这两种的区别
这两个方法的最主要区别在于run()方法的来源。
```java
@Override 
public void run() { 
    if (target != null) { 
        target.run(); 
    } 
}
```
实现Runnable的方式：最终调用target.run(); 
继承Thread类的方式：run()整个都被重写


## start()源码&原理
1. 首先判断线程状态是否为0
1. 加入线程组
1. 执行start0()方法

### 如果同一个线程执行两次start方法会发生什么？
会报异常，提示线程状态有问题。