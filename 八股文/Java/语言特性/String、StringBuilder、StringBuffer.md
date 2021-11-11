- [常见问题](#常见问题)
  - [String、StringBuilder、StringBuffer 的区别是什么？](#stringstringbuilderstringbuffer-的区别是什么)
- [公司](#公司)


</br></br>


# 常见问题
## String、StringBuilder、StringBuffer 的区别是什么？
答：
- String 是 `immutable` 的，每次的操作都会创建一个新的 String 对象，当操作频繁时会带来额外的开销（其实 JVM 会优化变成 StringBuilder）；
- StringBuilder、StringBuffer 内部维护了一个可变的字符数组，每次操作都是改变字符数组的状态，避免创建大量的 String 对象；
  - StringBuffer 是线程安全的，
  - StringBuilder 是线程不安全的。


</br></br>


# 公司