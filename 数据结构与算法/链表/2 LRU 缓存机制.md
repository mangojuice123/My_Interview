- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目

# Follow up
- LinkedList 分析：
    - HashMap 是一个无序的 Map，每次根据 key 的 hashcode 映射到 Entry 数组上，遍历全部元素的顺序并不是写入的顺序。
    - LinkedHashMap 基于 HashMap 实现，在前者的基础上增加了双向链表的实现，提供了两种排序方式：
        - 根据写入顺序排序（默认）；
        - 根据访问顺序排序（需要设置 accessOrder 为 true）。
    - 根据访问顺序排序时，每次 get 都会将访问的值移动到链表末尾。
      - 微信的转发消息机制就时 LRU 的一个应用。
- 实现线程安全的 LRU （get、put 方法加锁）。

# 测试用例

# 题解
```
class ListNode:
    """
    Double linked list node.
    """

    def __init__(self, key=0, value=0, prev=None, next=None) -> None:
        self.key = key
        self.value = value
        self.prev = prev
        self.next = next


class LRUCache:

    def __init__(self, capacity: int):
        self.size = 0
        self.capacity = capacity

        self.head = ListNode()
        self.tail = ListNode()
        self.head.next = self.tail
        self.tail.prev = self.head

        self.cache = {}

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1

        node = self.cache[key]
        self.moveToHead(node)
        return node.value

    def put(self, key: int, value: int) -> None:
        if key not in self.cache:
            node = ListNode(key=key, value=value)
            self.cache[key] = node
            self.addToHead(node)
            self.size += 1
            if self.size > self.capacity:
                removed = self.popTail()
                self.cache.pop(removed.key)
                self.size -= 1
        else:
            node = self.cache[key]
            node.value = value
            self.moveToHead(node)

    def addToHead(self, node):
        node.next = self.head.next
        node.prev = self.head
        self.head.next.prev = node
        self.head.next = node

    def removeNode(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev

    def moveToHead(self, node):
        self.removeNode(node)
        self.addToHead(node)

    def popTail(self):
        node = self.tail.prev
        self.removeNode(node)
        return node
```

# 复杂度
- 时间复杂度：`O(1)`
- 空间复杂度：`O(n)`

# 公司
- 2021-11 字节跳动
- 2021-9 阿里