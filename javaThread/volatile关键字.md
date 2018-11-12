于此处学习:

https://www.cnblogs.com/dolphin0520/p/3920373.html

https://www.cnblogs.com/chengxiao/p/6528109.html

此前需要了解
1. 简单了解Thread实现
2. 简单了解sychonized
3. 简单了解 java内存模型 并发编程三个属性概念

# 1. 功能

轻量级锁

多线程中使用

修饰静态变量和非静态变量

作用:

1. 保证了不同变量对共享变量的随时可见性,(这个写会操作会导致其他线程中的缓存无效。)
2. 禁止进行指令重排序

# 2. 可见性分析

可以保证可见性

因为 一旦标记的缓存中变量做出更改,会强制性刷新到主存中取,其他线程的缓存中的变量也会无效,需要重新去主存中取.

# 3. 原子性分析

``` java
public class Test {
    public volatile int inc = 0;
     
    public void increase() {
        inc++;
    }
     
    public static void main(String[] args) {
        final Test test = new Test();
        for(int i=0;i<10;i++){
            new Thread(){
                public void run() {
                    for(int j=0;j<1000;j++)
                        test.increase();
                };
            }.start();
        }
         
        while(Thread.activeCount()>1)  //保证前面的线程都执行完
            Thread.yield();
        System.out.println(test.inc);
    }
}
```

都使用这个做例子,说 inc++复合操作 操作不是原子性的. 会涉及三个步骤 :
1. 读取 inc
2. inc+1
3. 写入 inc

理由:
1. 线程A 读取inc(0),然后被阻塞,
2. 线程B读取inc(0),线程B执行inc+1,线程B执行 写入inc(1)
3. 线程A 执行inc+1
4. 线程A写入 inc(1)

结论执行完两个线程 inc值还是1

但是我对这里很疑惑呀...在执行3之前不是应该线程A中的缓存会失效么,重新读取inc值呀(根据上一条可见性规则),求大神指教.

# 4.有序性分析

可以保证一定程度上的 有序(禁止指令重排序功能)

``` java
x = 2;        //语句1
y = 0;        //语句2
volitile int flag = true;  //语句3
x = 4;         //语句4
y = -1;       //语句5
``` 
可以保证 语句3 一定是在 语句 1 2完毕 之后执行的,并且一定优先于语句 4 5

如果没有 语句3,那么 语句 1 2 4 5,执行的顺序是完全随机的.

禁止指令重排序功能
1. 保证 在之前的语句已经先于自己执行完毕
2. 保证自己一定先于 自己顺序之后的语句执行


后续还需要加深学习,目前仅初步了解作用.



