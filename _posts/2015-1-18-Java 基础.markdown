---
layout: post
title:  "Java 基础"
date:   2015-1-14 18:58:48
categories: [DevStudy]
---
# Java 基础

Tags:Java DevStudy

---

**转载请注明出处** [https://www.zybuluo.com/BookThief/note/63213](https://www.zybuluo.com/BookThief/note/63213)  --by [BookThief](http://weibo.com/nonboat/)

[TOC]

## 前言

　　Java的基础知识、Java EE的Web开发，都是在上学期间学习、实践的。因为毕业之后在银行做了柜员，很久没有再实际的进行过编码。如今在重新就业的当口，写一写总结、做一点练习项目，让自己更快的找回Coding的感觉。

　　针对Java Web的学习，我决定分3个部分来写笔记：I、Java基础;II、JSP + Servlet + JDBC;III、SSH + MyBatis(IBatis)框架。本篇是这个系列的第一部分，主要写我认为重要的Java基础知识、特性。

---

## 理论向

### 基本数据类型

| 基本数据类型 | 大小 | 默认值 | 包装类  |
|:------------:|:----:|:------:|:-------:| 
|    byte      |  8   |   0    |  Byte   |
|    short     |  16  |   0    |  Short  |
|    int       |  32  |   0    | Integer |
|    long      |  64  |   0    |  Long   |
|    float     |  32  |  0.0f  |  Float  |
|    double    |  64  |  0.0d  | Double  |
|    char      |  16  | \u0000 |Character|
|    boolean   |  1   | false  | Boolean |

　　8种基本数据类型，针对面试题的话，我看经常有根据数据位的大小，考向低位转化的。特别提一点，一般大小的整数，默认类型是int；一般的浮点数，默认类型是double。

　　8种基本类型，对应着8个包装类。听说主要是为了当初的承诺——Java中物物皆是对象。

    # 常用方法
    
    .MIN_VALUES                                             # 得到该类的最小值(boolean无)
    .MAX_VALUES                                             # 得到该类的最大值(boolean无)
    
    .typeValue()                                            # 转换成 type 类型的值 
    .toString()                                             # Type包装类 ==> 字符串(这个多余了)
    
    Type(String)                                            # 字符串 ==> Type包装类 I
    Type.parseType(String,radiX)                            # 字符串 ==> Type包装类 II
                                                            # radiX是指String为哪种进制的值
                                                            # JDK5 之后，有自动拆包/装包特性

　　最后特别说一点，Integer包装类有一个缓冲池(类似于String)，`-128 ~ 127`之间的值不会新建对象，都是直接引用。即对象取这之间的值，`==`结果为True(都说了，类似于String)。Boolean也差不多，直接创建了两个对象为"true","flase"，如果你new两个Boolean对象都赋值为"true"，他们的`==`结果也是true。

---

### OO(Object Oriented)特性 [^tag1]

　　我看但凡网络上涉及到JavaOO特性的，和学校老师所讲都不一样……老师说的是三个：封装、继承、多态。常见的是四个，+抽象。也不说谁对谁错，反正Java的抽象是一个很重要的特性，在JavaWeb开发中常用到。

    * 封装：是为了实现“高内聚、低耦合”，防止程序相互依赖性而带来的变动影响。即将对象封装成一个高度自治和相对封闭的个体，对象状态（属性）由这个对象自己的行为（方法）来读取和改变。

    * 继承：指派生类中包含了基类中的所有的行为（即方法）和状态（即变量），并能通过该派生类进行访问。继承的关键好处在于它提供了代码重用性和扩展性。但也有可能由于子类过度依赖父类，造成强耦合。

    * 多态：是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定。简而言之，即对象的定义可以是接口（父类），而实例可以是该接口（父类）的任意实现（子类）。可提供更泛化和弱耦合的代码。

    * 抽象：找出一些事物的相似和共性之处，然后将这些事物归为一个类，这个类只考虑这些事物的相似和共性之处，并且会忽略与当前主题和目标无关的那些方面，将注意力集中在与当前目标有关的方面。

___PS.抽象和封装的区别：(完全引用自[ImportNew - Java面试参考指南](http://www.importnew.com/12516.html)，写的十分经典，我觉得没法再简练的表达了，CP大法好)___

>　　封装作为一种策略，被用作广义抽象的一部分。封装是与对象状态相关的——对象将自己的状态封装起来并对外界不可见，类外部的用户只能通过该类的方法来与其进行交互，但不能直接改变其状态。因此，类可以将与状态相关的实施细节通过抽象隔离开来。
　　抽象是一个更泛化的概念，可以通过子类来实现具体的功能。例如：在Java标准库中，List是“一串事物”的抽象，ArrayList和LinkedList是List的两个具体的类型，作用于抽象List的代码同样抽象地不指明具体所使用的List类型。
　　如果没有通过封装隐藏底层状态，也就不可能进行抽象处理。也就是说，如果一个类的内部状态全部都是公开的，内部功能无法被更改，该类也就无法进行抽象。

---

### String | StringBuffer | StringBulider

|    对象类型   | 常量/变量  | 是否线程安全 | 速度 |
|:-------------:|:----------:|:------------:|:----:| 
|    String     | 字符串常量 |     --       | 较慢 |
| StringBuffer  | 字符串变量 |  线程安全    | 较快 |
| StringBuilder | 字符串变量 |  线程非安全  | 最快 |

　　之前提到Integer类有一个缓存池，String、StringBuffer、StringBuilder同样也有缓存池，但不像Integer那样是固定的256个数字。

　　String类会在编译时创建缓存池，缓存池内的对象都是不重复、不可改变的字符串(这也是String的`==`、`.equals()`常会混淆的地方)。如果值经常改变的对象使用String，会造成GC大量清理无用对象的工作，引起内存的大量使用。

　　StringBuffer、StringBuilder每次都对对象本身操作，而不生成新的对象，因此速度会快很多。StringBuilder因为不考虑多线程情况，速度最快。一般开发过程中，值经常改变的对象一般使用StringBuffer。

    # StringBuffer | StringBuilder 常用方法
    .append(String str)                                     # 尾部追加str
    .toString()                                             # 转换为String对象
    .insert(int offset,String str)                          # 在offset位置插入str
    .reverse()                                              # 字符串反转
    .delete(int start,int end)                              # 删除 startup ~ end-1 位置的字符

---

### Exception

![Exception](https://raw.githubusercontent.com/BookThief-D/pictures/master/Java/Java%E5%9F%BA%E7%A1%80/Exception.jpg "其实可以用Markdown的语法来画，但是Github上就不支持了")

　　Exception和Error都继承于Throwable类。Error是程序本身无法解决的问题，如栈溢出、线程死锁、内存泄漏；Exception是指程序能够可以处理、恢复的问题，包括CheckedException、UncheckedException。

　　UncheckedException就是指运行时异常(RuntimeException)，一般是由于开发者逻辑设计不当造成的、可避免的异常，由字面意义可知在编译时并不被检查，无论是否使用try-cache语句处理都会编译通过。CheckedException必须使用try-cache语句处理或用throws抛出给上层方法处理，否则编译无法通过。

    # 几个关键字的解释
    throws                                                  # 捕获并向上层方法抛出异常
    throw                                                   # 抛出一个异常

    try{                                                    # 通常由try块执行可能发生异常语句
    }cache(Exception e){                                    # cache执行捕获、抛出异常操作
    }finally{}                                              # finally一般用于DB、IO的关闭

---

### GC

　　GC(Gabage Collection)垃圾回收可以有效的防止内存泄露，有效的使用可以使用的内存。垃圾回收器通常是作为一个单独的低级别的线程运行，不可预知的情况下对内存堆中已经死亡的或者长时间没有使用的对象进行清楚和回收，程序员不能实时的调用垃圾回收器对某个对象或所有对象进行垃圾回收。回收机制有分代复制垃圾回收和标记垃圾回收，增量垃圾回收。

---

## 应用向

### IO

    * 根据处理数据类型的不同分为：字符流和字节流
    * 根据数据流向不同分为：输入流和输出流

　　字节流：I、以字节(byte == 8 bit)为单位处理数据；II、可处理任何类型的数据。

　　字符流：I、以字赴(根据码表映射字符)为单位；II、仅处理字符类型数据。

```Java
/*  IO的东西在我接触到的范围内,多是用于文件的读写。
    下面是一个最简易的文件读入与写入例子。
*/
import java.io.*;

public class ExceptionTest {

    public static void main(String[] args) throws IOException {

        String pathIn = "E:\\in.txt" ;
        String pathOut = "E:\\out.txt";
        BufferedReader in = new BufferedReader(new FileReader(pathIn));
//      这句是由系统输入读取字符
//      BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new FileWriter(pathOut));
        StringBuffer strb = new StringBuffer();

        try {
            String temp;
            while((temp = in.readLine()) != null){
                strb.append(temp);
                strb.append("\n");
                out.write(temp);
                out.newLine();
            }
        }
        catch(Exception e) {
            e.printStackTrace();
        }
        finally {
            in.close();
            out.close();
        }

    }
}
```

　　**IO的东西其实非常多，我所列的只是在我看来日常用得到的东西。**

　　特别提一下`BufferedReader | BufferedWriter`：各拥有8192字符的缓冲区。

　　当BufferedReader在读取文本文件时，会先尽量从文件中读入字符数据并置入缓冲区，而之后若使用read()方法，会先从缓冲区中进行读取。如果缓冲区数据不足，才会再从文件中读取，使用BufferedWriter时，写入的数据并不会先输出到目的地，而是先存储至缓冲区中。如果缓冲区中的数据满了，才会一次对目的地进行写出。

---

### Thread

**I、线程的创建与启动**

　　线程的实现方式有两种：继承Thread类;实现Runnabale接口

```Java
//线程的定义
public class MyThread extends Thread{
    @Override
    public void run() {
        //线程逻辑内容实现
    }
}

//线程的实例化
MyThread myThread = new MyThread();
//线程的启动
myThread.start();
```

```Java
//线程的定义
public class MyRunnable implements Runnable{
    @Override
    public void run() {
        //线程逻辑内容实现
    }
}

//线程的实例化
MyRunnable myRunnable = new MyRunnable();
Thread thread = new Thread(myRunnable);
//线程的启动
thread.start();
```

　　相比较而言，更推荐使用实现Runnable接口的方法，Runnable实现类内的资源可被共享(Thread的继承类内资源使用static关键字修饰也能达到同样效果，但不是一个好的习惯)。

**II、线程的生命周期**

![Thread-life](https://github.com/BookThief-D/pictures/blob/master/Java/Java%E5%9F%BA%E7%A1%80/Thread-life.jpg?raw=true "一图解千愁")

**III、synchronized**

* 当两个并发线程访问同一个对象object中的这个synchronized(this)同步代码块时，一个时间内只能有一个线程得到执行。另一个线程必须等待当前线程执行完这个代码块以后才能执行该代码块。

* 然而，当一个线程访问object的一个synchronized(this)同步代码块时，另一个线程仍然可以访问该object中的非synchronized(this)同步代码块。

* 尤其关键的是，当一个线程访问object的一个synchronized(this)同步代码块时，其他线程对object中所有其它synchronized(this)同步代码块的访问将被阻塞。

* 第三个例子同样适用其它同步代码块。也就是说，当一个线程访问object的一个synchronized(this)同步代码块时，它就获得了这个object的对象锁。结果，其它线程对该object对象所有同步代码部分的访问都被暂时阻塞。

* 以上规则对其它对象锁同样适用

---

### Collection

![Collection](https://github.com/BookThief-D/pictures/blob/master/Java/Java%E5%9F%BA%E7%A1%80/Collection.jpg?raw=true)

　　如图所示，前两行都是接口，下面两行都是类。

    下面按图内的相关性，做一下对比：
    
    * Collection是单个数据类型的容器，Map是< Key , Value >(键值对)类型的容器。
    * Set内无重复元素，List内允许有重复元素。
    * TreeSet默认会对元素进行自然序排序(也可以按需要重写排序规则)，HashSet速度快但无序。
    * LinkedList为链表实现，ArrayList、Vector为数组实现，Vector相对于ArrayList线程安全(实现了Serializable)。Stack后入先出的特性在一些算法里能得到很好的体现。
    * HashTable内不允许有空值(null)，且是线程安全的；HashMap是线程非安全的，< key , value >都允许空值；WeakHashMap是HashMap的改良版，对key实现弱引用，可被GC回收；TreeMap不同于于HashMap的地方在于实现了key值的自然序(或重写排序规则)的排序，key不允许有空元素而value允许。

**Collections**

　　与Collection不直接相关，只是一个不能被实例化的工具类。常用于搜索、排序、线程安全化。

　　其中，实现.sort()方法有两个办法：I、封装对象类内实现Comparable接口，重写compareTo()方法；II、创建一个实现Comparator接口的自定义类，重写compare()方法。因为实现Comparator接口在封装对象类之外，不破坏类的封装，且排序规则可根据需要创建多个自定义类，灵活方便。

**Iterator** [^tag2]

>迭代器是一种设计模式，它是一个对象，它可以遍历并选择序列中的对象，而开发人员不需要了解该序列的底层结构。迭代器通常被称为“轻量级”对象，因为创建它的代价小。
　　Java中的Iterator功能比较简单，并且只能单向移动：
(1) 使用方法iterator()要求容器返回一个Iterator。第一次调用Iterator的next()方法时，它返回序列的第一个元素。注意：iterator()方法是java.lang.Iterable接口,被Collection继承。
(2) 使用next()获得序列中的下一个元素。
(3) 使用hasNext()检查序列中是否还有元素。
(4) 使用remove()将迭代器新返回的元素删除。
　　Iterator是Java迭代器最简单的实现，为List设计的ListIterator具有更多的功能，它可以从两个方向遍历List，也可以从List中插入和删除元素。

---

## 参考资料

**[1]. [ImportNew](http://www.importnew.com/)**
**[2]. [CSDN](http://blog.csdn.net/)**
**[3]. [博客园](http://www.cnblogs.com/)**

***因参考文章众多，且部分无法找到原创连接(好多人写了转，却没添加转载链接，such as me)，仅列出文章的大概出处，有意者劳烦自己找一下。若原创作者认为本文有任何可能侵权行为，可发送邮件至`tjurac.gp@gmail.com`联系我，我会尽快删除内容或注明来源***


[^tag1]:本节（OO特性）内容，多引用自[ImportNew](http://www.importnew.com/12516.html)的阐述。

[^tag2]:本节（Iterator）内容，引用自[玉米疯收](http://www.cnblogs.com/amboyna/archive/2007/09/25/904804.html)的阐述。

**转载请注明出处** [https://www.zybuluo.com/BookThief/note/63213](https://www.zybuluo.com/BookThief/note/63213)  --by [BookThief](http://weibo.com/nonboat/)