- [MTU and MSS](#mtu-and-mss)

</br></br>

# MTU and MSS
- [MTU = Maximum transmission unit](https://developer.aliyun.com/article/222535)
- [MSS = Maximum segment size](https://www.zhihu.com/question/48454744/answer/110946313)
- MTU = TCP header + IP header + MSS
- 通信双方最终的 `MSS = min {本地物理接口 MTU 的限制, 对方声明的 MSS}`