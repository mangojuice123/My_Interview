- [常见问题](#常见问题)
  - [讲讲 volatile 关键字](#讲讲-volatile-关键字)
  - [讲讲 synchronized 关键字](#讲讲-synchronized-关键字)
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
    // 声明了一个 Singleton 类型的变量 singleton（还没有划分内存空间）。
    // volatile 关键字一定要加上！
    private static volatile Singleton singleton;

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


## 讲讲 synchronized 关键字
答：
- synchronized 实现原理：
  - 每个对象有一个监视器锁（monitor）。当 monitor 被占用时就会处于锁定状态，线程执行 `monitorenter` 指令时尝试获取 monitor 的所有权，过程如下：
    1. 如果 monitor 的进入数为 0，则该线程进入 monitor，然后将进入数设置为 1，该线程即为 monitor 的所有者。
    2. 如果线程已经占有该 monitor，只是重新进入，则进入 monitor 的进入数加 1。
    3. 如果其他线程已经占用了 monitor，则该线程进入阻塞状态，直到 monitor 的进入数为 0，再重新尝试获取 monitor 的所有权。
  - 执行 `monitorexit` 的线程必须是 `objectref` 所对应的 monitor 的所有者。
    - 指令执行时，monitor 的进入数减 1，如果减 1 后进入数为 0，那线程退出 monitor，不再是这个 monitor 的所有者。其他被这个 monitor 阻塞的线程可以尝试去获取这个 monitor 的所有权。 



</br></br>


# 公司