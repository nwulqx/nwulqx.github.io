---
title: 一道Java多线程问题
date: 2019-12-25 08:02:16
categories: 
- Java
tags:
- Java
- 多线程
- 并发
- 牛客网
---

# 背景

这道题在我2015年初学Java时遇到，至今已过去4年多了，也收到了200多的赞和很多回复，对我的Java学习起到了很好的正反馈作用，那么现在就来看下这道题目到底是怎么回事。



以下JAVA程序的输出是什么（）

```java
/*
 *https://www.nowcoder.com/questionTerminal/3b463ebec8404ad9b1b288859f124543?toCommentId=59907
 */
public class HelloSogou{
     public static synchronized void main(String[] a){
         Thread t=new Thread(){
             public void run(){Sogou();}
     };
     t.run();
     System.out.print("Hello");
     }
     static synchronized void Sogou(){
     System.out.print("Sogou");
    }
}
```
```java
A. HelloSogou
B. SogouHello
C. Hello
D. 结果不确定
```
<!-- more -->
# 解析

第一，我觉得误区有两个：一个是run和start区别，`Thread.run()`是调用方法，`Thread. start()`是启动线程；另一个是锁持有问题。这个题是调用方法，和多线程就无关。本题只有一个线程，持有HelloSogou.class锁。那么，就是第二个问题了：同步方法调用另一个同步方法的锁问题？

```java
 public synchronized void  methodA(int a, int b){}
 public synchronized void methodB(int  a）{
    methodA(a, 0); 
  }
```
首先要明白两个问题，**1.锁的对象是谁？2.谁持有了锁？**

假设方法A和B是在同一个类Test中的两个方法。

```java
Test  t=new Test(); 
t.methodB(); 
```

调用methodB()方法，获得锁，锁是对象`t`；锁谁持有？当前线程（不可以说是methodB持有该锁），methodB又调用methodA，也需要锁`t`，该线程已持有`t`，当然可以直接调用methodA。 

类比到此题，只有一个主线程，调用main，持有`HelloSogou.class`锁，那当然可以直接调用Sogou方法。



第二，如果是`t.statrt()`，那么这个题，**静态同步函数的锁是该类的字节码文件.class。**此题中，main函数和Sogou方法都是static的，所以持有相同`锁 HelloSogou.class`，那么，在main线程（main  是一个线程也是一个进程  ）中又开了一个线程，调用Sogou方法，锁会冲突。

所以我的分析是：调用main函数（一个线程），main函数开启另一个线程，并启动，但是main函数和Sogou方法是同一个锁，所以main函数执行完毕后才会释放锁，Sogou方法才会执行，这就是为什么，换成start，是HelloSogou。 



第三，将Sogou方法的锁改为其他.class锁，那么，HelloSogou和SogouHello都可能出现。因为没有互斥现象了，变为`抢占式`的了。