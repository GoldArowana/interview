# 实现多线程

## 实现多线程有几种方法

Oracle官方的解释是两种。

### 继承Thread类

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

### 实现Runnable接口









