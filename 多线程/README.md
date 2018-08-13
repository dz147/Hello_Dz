# 多线程
### Thread和Runnable的区别
- 如果一个类继承Thread，则不适合资源共享。
-  但是如果实现了Runable接口的话，
-  则很容易的实现资源共享。
### 获得随机数
- 方法1(数据类型)(最小值+Math.random()*(最大值-最小值+1))
- 方法2 获得随机数

      for (int i=0;i<30;i++)
      {System.out.println((int)(1+Math.random()*10));}
      (int)(1+Math.random()*10)
      
    通过java.Math包的random方法得到1-10的int随机数
      公式是:最小值---最大值（整数）的随机数
      （类型）最小值+Math.random()*最大值
#### StringBuffer与多线程实例
public class DemoString {

    public static void main(String[] args) {
        Test1 str = new Test1();
        //创建了多个线程 异步
        for (int i = 1; i <= 3 ; i++) {
            Thread thread=new Thread(new MyRunnable(str));
            thread.start();
        }
        System.out.println("理应结果为600000(并行执行的，资源存在争用的问题)");
    }
}

class Test1 {
    
    public StringBuilder str=new StringBuilder();
    //public StringBuffer str=new StringBuffer();//有很多方法
}

class MyRunnable implements Runnable {

    Test1 strb;
    public MyRunnable(Test1 number) {
        this.strb = number;
    }
    @Override
    public void run() {
        counter();
    }
    //封装counter();
    public  void counter() {
        for (int i = 0; i < 200000; i++) {
            strb.str.append("r");
        }
        System.out.println("多线程分段累加为：" + strb.str.length());
    }
}
- 
###  线程类的一些常用方法
- sleep(): 强迫一个线程睡眠Ｎ毫秒。 
- isAlive(): 判断一个线程是否存活。 
- join(): 等待线程终止。 
- activeCount(): 程序中活跃的线程数。 
- enumerate(): 枚举程序中的线程。 
- currentThread(): 得到当前线程。 
- isDaemon(): 一个线程是否为守护线程。 
- setDaemon(): 设置一个线程为守护线程。(用户线程和守护线程的区别在于，是否等待主线程依赖于主线程结束而结束) 
- setName(): 为线程设置一个名称。 
- wait(): 强迫一个线程等待。 
- notify(): 通知一个线程继续运行。 
- setPriority(): 设置一个线程的优先级
- start()和run()方法
-  如果执行start方法，则会在主线程中重新创建一个新的线程，
等得到cpu的时间段后则会执行所对应的run方法体的代码。
- Volatile 变量可用于提供线程安全
- 线程出问题 则
- 如果该异常被捕获或抛出，则程序继续运行。 
- 如果异常没有被捕获该线程将会停止执行。 
### 多线程面试题
- https://www.cnblogs.com/zjdxr-up/p/6638131.html

### 线程概要
- 线程:进程的一个实体,是CPU调度和分派的基本单位,它是比进程更小的能独立运行的基本单位.线程自己基本上不拥有系统资源,
只拥有一点在运行中必不可少的资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源.
### 区别进程线程
1) 简而言之,一个程序至少有一个进程,一个进程至少有一个线程.

2) 线程的划分尺度小于进程，使得多线程程序的并发性高。

3) 另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。

4) 线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。
但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。

5) 从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。
但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别。
### 线程安全总结
- 如果你的代码所在的进程中有多个线程在同时运行，
- 而这些线程可能会同时运行这段代码。
- 如果每次运行结果和单线程运行的结果是一样的，
- 而且其他的变量的值也和预期的是一样的
### 线程同步
- 在多线程应用中，考虑不同线程之间的数据同步和防止死锁。
- 当两个或多个线程之间同时等待对方释放资源的时候就会形成线程之间的死锁。
- 为了防止死锁的发生，需要通过同步来实现线程安全。
- 在Java中可用synchronized关键字。

#### 死锁是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象

### StringBuffer 与StringBuilder
#### 速度 StringBuilder > StringBuffer > String
- String为常量 StringBuffer/StringBuilder为变量
- 在线程安全上，StringBuilder是线程不安全的，
- 而StringBuffer是线程安全的
- 如果一个StringBuffer对象在字符串缓冲区被多个线程使用时，
- StringBuffer中很多方法可以带有synchronized关键字，
- 所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，
- 所以不能保证线程安全，有可能会出现一些错误的操作。
- 所以如果要进行的操作是多线程的，那么就要使用StringBuffer，
- 但是在单线程的情况下，还是建议使用速度比较快的StringBuilder。
### 单例模式
- 每个单例模式的对象都是存储在静态共享区中！
