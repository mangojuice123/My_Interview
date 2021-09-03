- [Java Language](#java-language)
    - [1. 覆盖和重载的区别](#1-覆盖和重载的区别)
    - [2.（堆）内存泄漏和内存溢出的区别、原因、举例](#2堆内存泄漏和内存溢出的区别原因举例)
  - [3. 内存泄漏的增多，最终会导致内存溢出](#3-内存泄漏的增多最终会导致内存溢出)
- [Java Multithreading](#java-multithreading)
    - [1. 进程与线程的区别](#1-进程与线程的区别)
    - [2. 为什么使用锁来同步和保护资源](#2-为什么使用锁来同步和保护资源)
- [TCP/IP](#tcpip)
    - [1. Web 的攻击技术](#1-web-的攻击技术)
    - [2. HTTP 与 HTTPS 的区别](#2-http-与-https-的区别)
    - [3. HTTPS 的实现](#3-https-的实现)

# Java Language
### 1. 覆盖和重载的区别
1. Overloading
    - 多个方法可以共享一个方法名，但是每个方法各自的参数不同，值得注意的是函数签名并不包括返回值类型，即不能通过只改变返回值类型来重载函数。
    - 比较典型的例子就是整型数字与整型数字相加的方法，浮点数与浮点数相加的方法，二者使用不同的参数，有着不同的返回值，却有着相同的方法名称。

    ```
    int myMethod(int x, int y) { }
    double myMethod(double x, double y) { }
    ```
2. Overriding
    - 在某些特定情况下用一个实现替换另一个实现。覆盖一般是子类重新定义继承下来的方法，以改变或延伸此方法的行为。
    - Java 5 之前覆盖返回的类型必须一致，Java 5 之后覆盖函数的返回类型可以是基类方法返回值的派生类型。

    ```
    public class AnimalNoise {}
    public class Miaw extends AnimalNoise {}

    public class Animal {
        public AnimalNoise makeNoise() {
            return new AnimalNoise();
        }
    }

    public class Cat extends Animal {
        public Miaw makeNoise() {
            return new Miaw();
        }
    }
    ```
3. 多态
    - 一个类的多态性用 `Overloading` 来表现
    - 子类与父类的多态性用 `Overriding` 来表现

### 2.（堆）内存泄漏和内存溢出的区别、原因、举例
1. Memory Leak
    - 导致 `OutOfMemory` 异常的对象是不必要的（应该被垃圾回收但是没被回收的）
    - 原因
        1. 循环过多或死循环，产生了大量的对象
        2. 静态集合类引起内存泄漏，因为静态集合的生命周期和 JVM 一致，所以静态集合引用的对象不能被释放
        3. 单例模式，生命周期和 JVM 一致，如果单例对象持有外部对象的引用，那么这个外部对象也不会被回收
        4. 内部类的对象被长期持有，那么内部类对象所属的外部类对象也不会被回收
        5. `Hash` 值发生改变

    ```
    import java.util.*;
    public class Main {
        static class OOMObject {}

        public static void main(String[] args) {
            List<OOMObject> list = new ArrayList<OOMObject>();

            while (true) {
                list.add(new OOMObject());
            }
        }
    ```
2. Memory Overflow
    - 导致 OutOfMemory 异常的对象是必要的。（申请内存时，没有足够的内存可用）
    - 原因
        - Java 虚拟机的堆参数 `-Xmx -Xms` 设置过小 ---> `java -Xms1m -Xmx1m xxx.java`
        - 代码中不合理的设计如对象生命周期过长、持有状态时间过长、存储结构设计不合理等情况
3. 内存泄漏的增多，最终会导致内存溢出
---
# Java Multithreading

### 1. 进程与线程的区别
1. 进程与线程最大的区别就是**内存是否共享**
    - 每个进程都拥有彼此独立的内存空间
    - 线程之间共享内存（Java 内存模型中包含共享内存和缓存这两种内存。其中，线程之间共享的是共享内存）
        - 由于线程之间共享内存，所以线程之间的通信可以很自然、简单地实现
        - 一个线程向实例中写入内容，其他线程就可以读取该实例的内容
2. 线程的上下文切换比进程快
    - 当执行紧密关联的多项工作时，通常线程比进程更加合适

### 2. 为什么使用锁来同步和保护资源
1. [race condition](https://stackoverflow.com/questions/34510/what-is-a-race-condition)
    - 当有多个线程存在，并且在同一时间访问共享数据时，会造成 race condition
    - 看起来好像这些线程在比赛抢着去访问这些数据一样

    ```
    if (x == 5) // The "Check"
    {
        // If another Thread changed x in between
        // y will not be equal to 10.

        y = x * 2; // The "Act"
    }
    ```
2. 死锁
    - ![死锁](https://user-images.githubusercontent.com/57697266/132002155-d30e4a04-8834-484e-a1cb-14383fe8ec25.png)

    ```
    new EaterThread("Alice", spoon, fork).start();
    new EaterThread("Bobby", fork, spoon).start();
    
    class EaterThread extends Thread {
        private final Tool leftHand;
        private final Tool rightHand;
        public EaterThread(Tool leftHand, Tool rightHand) {
            this.leftHand = leftHand;
            this.rightHand = rightHand;
        }

        @Override
        public void run() {
            while (true) {
                eat();
            }
        }

        public void eat() {
            synchronized(leftHand) {
                // 使用左边的餐具
                synchronized(rightHand) {
                    // 使用右边的餐具
                }
            }
        }
    }
    ```
---
# TCP/IP

### 1. Web 的攻击技术
1. 主动攻击：直接对服务器上对资源进行攻击，比较有代表性的是 `SQL 注入攻击` 和 `OS 命令注入攻击` 
    - SQL Injection 
        1. SQL Injection Based on `1 = 1` is Always True

        ```
        TxtUserID = getRequestString("UserID");
        txtSQL = "SELECT * FROM user WHERE user_id = " + txtUserId;
        ``` 

        ```
        > UserID: 105 OR 1 = 1
        SELECT * FROM user WHERE user_id = 105 OR 1 = 1;
        ```
        2. SQL Injection Based on `"" = ""` is Always True
        3. SQL Injection Based on Batched SQL Statements
        
            ```
            > UserID: 105; DROP TABLE suppliers;
            ```
    - Use SQL Parameters for Protection

        ```
        txtUserId = getRequestString("UserId");
        txtSQL = "SELECT * FROM user WHERE user_id = @0";
        db.Execute(txtSQL, txtUserId);
        ```
2. 被动攻击：攻击者不直接对目标 Web 应用发起攻击，而是诱使用户触发已经设置好的陷阱，获取用户的资源和权限，比较有代表性的是跨站脚本攻击（XSS）和跨站点请求伪造

### 2. HTTP 与 HTTPS 的区别
- HTTP + 通信加密 + 证书认证 + 完整性保护 = HTTPS
- HTTP主要有这些不足：
    1. 通信使用明文 -> 窃听
    2. 不验证通信方的身份 -> 伪装
    3. 无法验证报文的完整性 -> 篡改

### 3. HTTPS 的实现