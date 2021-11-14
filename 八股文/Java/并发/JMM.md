- [常见问题](#常见问题)
  - [讲讲 volatile 关键字](#讲讲-volatile-关键字)
- [公司](#公司)


</br></br>


# 常见问题
## 讲讲 volatile 关键字
答：
1. 防止指令重排序
    - 实例化一个对象可以分为三个步骤：
        - 分配内存空间；
        - 初始化对象；
        - 将内存空间的地址赋值给对应的引用。
    - 但是由于操作系统可以对指令进行重排序，所以上面的过程可能也会变成如下过程：
        - 分配内存空间；
        - 将内存空间的地址赋值给对应的引用。
        - 初始化对象。
    - 如果在本线程内观察，所有的操作都是有序的（Within-Thread As-If-Serial Semantics）；如果在一个线程中观察另一个线程，所有的操作都是无序的（指令重排序以及工作内存与主存同步延迟）。
    - 通过底层中的「内存屏障」实现。
```
public class Singleton {
    public static volatile Singleton singleton;

    /**
     * 构造函数私有，禁止外部实例化。
     */
    private Singleton() {};

    /**
     * 双重检查加锁，实现并发环境下的单例模式。
     */
    public static Singleton getInstance() {
        if (singleton == null) {
            synchronized (singleton) {
                if (singleton == null) {
                    singleton = new Singleton();
                }
            }
        }
        return singleton;
    }
}
```
2. 实现可见性
   - 可见性问题主要指一个线程修改了共享变量值，而另一个线程却看不到。
   - 引起可见性问题的主要原因是，每个线程拥有自己的一个高速缓存区——线程工作内存。
   - 实现方式：
     - 修改 `volatile` 变量时会强制将修改后的值刷新的主内存中；
     - 修改 `volatile` 变量后会导致其他线程工作内存中对应的变量值失效。因此，再读取该变量值的时候就需要重新读取主内存中的值。
3. 保证原子性：volatile 能保证对单次读/写的原子性。


</br></br>


# 公司