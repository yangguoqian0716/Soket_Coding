# 网络套接字Socket
## 讨论：跨主机的传输套注意的问题
### 字节序问题
1. 大小端存储问题
   - 问题：文件传输时，永远是低地址处的数据先发送出去，接收端以大端存储和小端存储的格式存储，天差地别
   - 解决方案：不区分大小端，采用主机字节序（host）和网络字节序（network）
   - 字节序转换函数：
       - 当前pc将数据传输给网络：host->net:**htons\htonl**
       - 当前pc从网络接收数据：net->host:**ntohs\ntohl**
  - IP地址点分式与大整数的转换函数：inet_pton、inet_ntop(专用于Ipv4和Ipv6)
2. 对齐问题： 解决方案：不对齐（让编译器不对齐的宏：**__attribute__((packed)**）
3. 类型长度问题
   - 问题：不同主机上int长度不同
   - 解决：通用类型：int32_t,uint32_t,int64_t,uint64_t,int8_t,uint8_t...

## socket是什么
Socket 是计算机网络中用于通信的一种编程接口。它是应用层与传输层之间的一个抽象，允许应用程序通过
网络进行数据传输。Socket在网络编程中非常重要，因为它提供了在不同主机或设备之间发送和接收数据的方法。
## 报式套接字
### 被动端（先运行）
1. 取得socket：socket函数
2. 给Socket取得地址：bind
3. 收/发消息：recvfrom
4. 关闭Socket: close

### 主动端（bind可以省略）
1. 取得socket: socket 
2. 给Socket取得地址（略）: bind
3. 收/发消息：sendto()
4. 关闭Socket: close
### Linux命令
- 查看udp状态：**netstat -anu**
- 查看当前系统路由表：**ip ro sh**
- 将默认网关设置为某个IP地址： **route add default gw <addr>**

### 多点通讯
广播（全网广播、子网广播），多播/组播
- setsocketopt
- getsocketopt
## 流式套接字
