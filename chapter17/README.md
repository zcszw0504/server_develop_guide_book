# 17 TCP的长连接和短连接


&emsp;&emsp;我们再来回顾一下TCP协议，使用TCP协议时，会在客户端和服务器之间建立一条虚拟的信道，这条虚拟信道就是指连接，而建议这条连接需要3次握手，拆毁这条连接需要4次挥手，可见，我们建立这条连接是有成本的，这个成本就是效率成本，简单点说就是时间成本，你要想发送一段数据，必须先3次握手（来往3个包），然后才能发送数据，发送完了，你需要4次挥手（来往4个包）来断开这个连接。  

&emsp;&emsp;其二，CPU资源成本，三次握手和4次挥手和发送数据都是从网卡里发送出去和接收的，还有其余的设备，比如防火墙，路由器等等，站在操作系统内核的角度来讲，如果我们是一个高并发系统的话，如果大量的数据包都经历过这么一个过程，那是很耗CPU的。

&emsp;&emsp;其三，每个socket是需要耗费系统缓存的，比如系统提供了一些接口设置socket缓存的，比如：
```
/proc/sys/net/ipv4/tcp_rmem
/proc/sys/net/ipv4/tcp_wmem
/proc/sys/net/ipv4/tcp_mem

```

&emsp;&emsp;因为TCP的可靠传输，所以我们有大量的应用程序使用TCP协议作为通信，但是每个应用因为产品功能的原因，对TCP的使用是不一样的，比如即时聊天系统（微信，钉钉，探探），比如另外一类

