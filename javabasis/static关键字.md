learn from [海子](https://www.cnblogs.com/dolphin0520/p/3799052.html)


# 目录
1. static用途
2. static关键字舞曲
3. 常见的笔试面试题
---
# 1.static关键字的用途

在方便没有创建对象的情况下进行调用

也可以 优化程序性能
``` java
    package JavaStatic.learnFromWeb;

    public class StaticLearn1 {
    
        public static int param1 = 0;
    
        public int param2 = 1;
    
        //静态方法只能调用静态方法和静态变量
        public static int getParam1(){
            System.out.println(param1);
            //无法调用非静态变量
            // System.out.println(param2);
            getParam1();
            //无法调用非静态方法 
            // getParam2(); 
            return param1;
        }
    
        //都可以调用
        public int getParam2(){
            System.out.println(param1);
            System.out.println(param2);
            getParam1();
            getParam2();
            
            return param2;
        }
        
        public static void main(String [] args){
            //可以直接调用
            int test1 = getParam1();
            //非静态方法无法在对象被构造之前被调用
            // int test2 =getParam2();
            StaticLearn1 staticLearn1 = new StaticLearn1();
            int test2 = staticLearn1.getParam2();
            
        }
    
    }
```
## 1.1 static方法

1. static方法也称为静态方法
2. 静态方法不依赖与任何对象 可以直接调用

            //可以直接调用
            int test1 = getParam1();

3. 由于不依赖对象 所以也无法调用对象中的非静态变量和非静态方法

        //静态方法只能调用静态方法和静态变量
        public static int getParam1(){
            System.out.println(param1);
            //无法调用非静态变量
            // System.out.println(param2);
            getParam1();
            //无法调用非静态方法 
            // getParam2(); 
            return param1;
        }

## 1.2 static变量
1. static变量称为静态变量
2. 静态变量被所有对象共享,内存中只有一个副本(非静态变量为对象拥有的,在构造对象的时候被初始化,可以有多个副本)
 

## 1.3 static代码块
其中非常大的一个用途为此项 以优化程序性能

例子:

    class Person{
        private Date birthDate;
         
        public Person(Date birthDate) {
            this.birthDate = birthDate;
        }
         
        boolean isBornBoomer() {
            Date startDate = Date.valueOf("1946");
            Date endDate = Date.valueOf("1964");
            return birthDate.compareTo(startDate)>=0 && birthDate.compareTo(endDate) < 0;
        }
    }
    
isBornBoomer是用来这个人是否是1946-1964年出生的，而每次isBornBoomer被调用的时候，都会生成startDate和birthDate两个对象，造成了空间浪费，如果改成这样效率会更好：

例子:

    class Person{
        private Date birthDate;
        private static Date startDate,endDate;
        static{
            startDate = Date.valueOf("1946");
            endDate = Date.valueOf("1964");
        }
         
        public Person(Date birthDate) {
            this.birthDate = birthDate;
        }
         
        boolean isBornBoomer() {
            return birthDate.compareTo(startDate)>=0 && birthDate.compareTo(endDate) < 0;
        }
    }

---

# 2. Static关键字的误区

1. static关键字可以更改访问权限么?

无法更改,只有 private protected public default 可以更改


权限     | 类内|同包|不同包子类|不同包非子类
:--:      |:--:|:--:|:--:|:--:
private  |√|×|×|×
default  |√|√|×|×
protected|√|√|√|×
public   |√|√|√|√


2.能通过this访问静态变量吗?

    public class Main {　　
        static int value = 33;
     
        public static void main(String[] args) throws Exception{
            new Main().printValue();
        }
     
        private void printValue(){
            int value = 3;
            System.out.println(this.value);
        }
    }
    


这里面主要考察队this和static的理解。this代表什么？this代表当前对象，那么通过new Main()来调用printValue的话，当前对象就是通过new Main()生成的对象。而static变量是被对象所享有的，因此在printValue中的this.value的值毫无疑问是33。在printValue方法内部的value是局部变量，根本不可能与this关联，所以输出结果是33。在这里永远要记住一点：静态成员变量虽然独立于对象，但是不代表不可以通过对象去访问，所有的静态方法和静态变量都可以通过对象访问（只要访问权限足够）

如果输出不是this.value  而是value的话 就是3
    


    输出结果:
    
    33
    
3. static可以用于局部变量吗

不可以规则规定的.


---
# 3.常见的笔试面试题

1. 一下代码输出结果是什么

``` java
    public class Test extends Base{
     
        static{
            System.out.println("test static");
        }
         
        public Test(){
            System.out.println("test constructor");
        }
       public static void main(String[] args) {
                new Test();
            }
    }
    
    class Base{
         
        static{
            System.out.println("base static");
        }
         
        public Base(){
            System.out.println("base constructor");
        }
    }
```
分析:
1. 先找到main方法
2. 在执行main方法之前需要先加载test类
3. test类又继承自base类,所以先加载base类
4. 发现base类中 有static方法      执行static
5. base加载后 发现test中也有static    执行static
6. 加载完成后 执行main函数 调用test构造器,但是先要执行base构造器
7. 执行test构造器


    输出结果:
    base static
    test static
    base constructor
    test constructor
    
2. 这段代码输出结果?

    ``` java
    public class Test {
        Person person = new Person("Test");
        static{
            System.out.println("test static");
        }
         
        public Test() {
            System.out.println("test constructor");
        }
         
        public static void main(String[] args) {
            new MyClass();
        }
    }
    
    class Person{
        static{
            System.out.println("person static");
        }
        public Person(String str) {
            System.out.println("person "+str);
        }
    }
     
     
    class MyClass extends Test {
        Person person = new Person("MyClass");
        static{
            System.out.println("myclass static");
        }
         
        public MyClass() {
            System.out.println("myclass constructor");
        }
    }
    ```


    输出结果:
    test static
    myclass static
    person static
    person Test
    test constructor
    person MyClass
    myclass constructor
