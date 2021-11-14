- [常见问题](#常见问题)
  - [讲讲 Java 内存模型与线程](#讲讲-java-内存模型与线程)
- [公司](#公司)


</br></br>


# 常见问题
## 讲讲 Java 内存模型与线程
答：
1. volatile
    - 某个线程对 volatile 字段进行的写操作结果对其他线程立即可见
    - [禁止指令重排序优化（对象的构造过程不是原子性的）](https://www.cnblogs.com/paddix/p/5428507.html)
    - [单例模式的线程安全](https://zhuanlan.zhihu.com/p/52316864)
    ```
    public class Singleton {
        private volatile static Singleton instance; // 注意 volatile 关键字 

        public static Singleton getInstance() {
            if (instance == null) {
                synchronized (Single.class) {
                    if (instance == null) {
                        // 如果没有 volatile 关键字，那么执行对象构造的过程中可能出现指令重排
                        instance = new Singleton(); 
                    }
                }
            }
            return instance;
        }
    }
    ```
2. 原子性、可见性与有序性
    - 原子性：基本数据类型的访问、读写都是具备原子性的
    - 可见性：当一个线程修改了共享变量的值时，其他线程能立即得知这个修改
        - volatile
        - synchronized
        - final
    - [有序性](https://stackoverflow.com/questions/16213443/instruction-reordering-happens-before-relationship-in-java)：如果在本线程内观察，所有的操作都是有序的（Within-Thread As-If-Serial Semantics）；如果在一个线程中观察另一个线程，所有的操作都是无序的（指令重排序以及工作内存与主存同步延迟）


</br></br>


# 公司