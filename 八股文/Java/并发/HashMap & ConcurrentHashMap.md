- [HashMap](#hashmap)
- [ConcurrentHashMap](#concurrenthashmap)
- [常见问题](#常见问题)
  - [HashMap 扩容机制是什么？为什么 HashMap 一般要初始化一个大小？](#hashmap-扩容机制是什么为什么-hashmap-一般要初始化一个大小)


</br></br>


# HashMap
- 1.7
![1.7](https://i.loli.net/2019/05/08/5cd1d2be77958.jpg)
- 1.8
![1.8](https://i.loli.net/2019/05/08/5cd1d2c1c1cd7.jpg)
- [单链表的头插法与尾插法](https://segmentfault.com/a/1190000021501440)


</br></br>


# ConcurrentHashMap


</br></br>


# 常见问题
## HashMap 扩容机制是什么？为什么 HashMap 一般要初始化一个大小？
答：
1. 什么时候扩容：当数据量达到 （当前容量 * 负载因子） 时，会触发 HashMap 的自动扩容。HashMap 的容量只能为 2 的幂，扩容时，新容量变为旧容量的 2 倍，并重新定位每个桶的下标，采用头插法（1.7）或尾插法（1.8）将元素迁移到新数组中。
2. 扩容带来的线程不安全：1.7 版本中，由于头插法迁移链表（链表的头插法类似于栈的先进后出，插入顺序与遍历结果相反），导致在并发情况下可能生成环形链表，导致死循环问题。
3. 扩容导致性能下降：扩容的过程需要 rehash、复制数据等操作，非常消耗性能，所以 HashMap 一般需要选择一个合适初始容量大小（`InitialCapacity = (需要存储的元素个数 / 负载因子) + 1`），避免频繁的扩容操作导致的性能下降。
