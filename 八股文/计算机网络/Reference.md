- [应用层](#应用层)
  - [HTTP](#http)
    - [GET 与 POST](#get-与-post)
    - [Cookie](#cookie)
    - [HTTP keep-alive](#http-keep-alive)
  - [HTTPS](#https)
    - [TLS](#tls)
- [传输层：对传输行为进行控制](#传输层对传输行为进行控制)
  - [TCP](#tcp)
    - [3-way handshake](#3-way-handshake)
    - [4-way handshake](#4-way-handshake)
  - [UDP](#udp)
- [网络互连层：将 TCP 层传下来的数据加上目标地址和源地址](#网络互连层将-tcp-层传下来的数据加上目标地址和源地址)
- [数据链路层](#数据链路层)
  - [MTU and MSS](#mtu-and-mss)


</br></br>


# 应用层
## HTTP
```
1. HTTP 请求报文

<METHOD> <URL> HTTP/1.1\r\n
<Header1>: <HeaderValue1>\r\n
<Header2>: <HeaderValue2>\r\n
...
<HeaderN>: <HeaderValueN>\r\n
\r\n
<Body Data....>

2. HTTP 响应报文

HTTP/1.1 <Code> <Phrase>\r\n
<Header1>: <HeaderValue1>\r\n
<Header2>: <HeaderValue2>\r\n
...
<HeaderN>: <HeaderValueN>\r\n
\r\n
<Body Data....>
```
### GET 与 POST
- [GET 与 POST 的区别](https://www.zhihu.com/question/28586791/answer/767316172)
- [URL 编码](http://www.ruanyifeng.com/blog/2010/02/url_encoding.html)

### Cookie
- [Cookie 与 Session 的区别](https://www.zhihu.com/question/19786827/answer/84540780)
- [Set-Cookie 与 Cookie](https://stackoverflow.com/questions/38485028/what-is-the-difference-between-set-cookie-and-cookie)

### HTTP keep-alive
- [HTTP keep-alive 和 TCP keepalive](https://www.geek-share.com/detail/2795504664.html)

## HTTPS
### TLS
- [TLS 握手流程](https://zhuanlan.zhihu.com/p/86304211)
- [TLS 协议](https://cshihong.github.io/2019/05/09/SSL%E5%8D%8F%E8%AE%AE%E8%AF%A6%E8%A7%A3/)


</br></br>


# 传输层：对传输行为进行控制
## TCP
![TCP header](https://upload.wikimedia.org/wikipedia/commons/d/da/TCP_header.png)
### 3-way handshake
- [通俗易懂的三握手和四挥手](https://mp.weixin.qq.com/s/u56NcMs68sgi6uDpzJ61yw)
- [RFC 793](https://www.ietf.org/rfc/rfc793.txt)
- [TCP 的 5 种报文及为什么是三次握手](https://mp.weixin.qq.com/s/NIjxgx4NPn7FC4PfkHBAAQ)
- [TCP connection status](https://www.ibm.com/docs/en/zos/2.1.0?topic=SSLTBW_2.1.0/com.ibm.zos.v2r1.halu101/constatus.htm)
- [TCP 状态转换图总结](https://zhuanlan.zhihu.com/p/78540103)
- [信道不可靠，但是通信双方需要就某个问题达成一致](https://groups.google.com/g/pongba/c/kF6O7-MFxM0/m/5S7zIJ4yqKUJ)
- [Two General's Problem](https://en.wikipedia.org/wiki/Two_Generals%27_Problem)
### 4-way handshake 
- [TIME_WAIT = 2 MSL(Maximum Segment Lifetime)](https://www.zhihu.com/question/67013338/answer/2005038284)
- [TIME_WAIT = 2 MSL 解决了什么问题](https://cloud.tencent.com/developer/article/1450264)

## UDP
![UDP header](https://upload.wikimedia.org/wikipedia/commons/0/0c/UDP_header.png)


</br></br>


# 网络互连层：将 TCP 层传下来的数据加上目标地址和源地址
![IP header](https://upload.wikimedia.org/wikipedia/commons/thumb/6/60/IPv4_Packet-en.svg/1280px-IPv4_Packet-en.svg.png)


</br></br>


# 数据链路层
![Ethernet Type Frame](https://upload.wikimedia.org/wikipedia/commons/thumb/1/13/Ethernet_Type_II_Frame_format.svg/1280px-Ethernet_Type_II_Frame_format.svg.png)
## MTU and MSS
- [MTU = Maximum transmission unit](https://developer.aliyun.com/article/222535)
- [MSS = Maximum segment size](https://www.zhihu.com/question/48454744/answer/110946313)
- MTU = TCP header + IP header + MSS
- 通信双方最终的 `MSS = min {本地物理接口 MTU 的限制, 对方声明的 MSS}`