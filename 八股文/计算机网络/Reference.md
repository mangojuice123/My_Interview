- [传输层](#传输层)
  - [3-way handshake](#3-way-handshake)
- [数据链路层](#数据链路层)
  - [MTU and MSS](#mtu-and-mss)

</br></br>

# 传输层
## 3-way handshake
- [为什么是三次](https://www.zhihu.com/question/24853633/answer/115173386)
- [TCP connection status](https://www.ibm.com/docs/en/zos/2.1.0?topic=SSLTBW_2.1.0/com.ibm.zos.v2r1.halu101/constatus.htm)
- [信道不可靠，但是通信双方需要就某个问题达成一致](https://groups.google.com/g/pongba/c/kF6O7-MFxM0/m/5S7zIJ4yqKUJ)
- [Two General's Problem](https://en.wikipedia.org/wiki/Two_Generals%27_Problem)


# 数据链路层
## MTU and MSS
- [MTU = Maximum transmission unit](https://developer.aliyun.com/article/222535)
- [MSS = Maximum segment size](https://www.zhihu.com/question/48454744/answer/110946313)
- MTU = TCP header + IP header + MSS
- 通信双方最终的 `MSS = min {本地物理接口 MTU 的限制, 对方声明的 MSS}`