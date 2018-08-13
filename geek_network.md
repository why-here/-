2. 分层

- 复杂的程序都要分层

#### 3. ifconfig

- ifconfig or ip addr
- nettools(bsd) ：通过 proc / ioctl 读写配置；iproute2 通过 netlink 套接字与内核通信
- CIDR 无类型域间选路 ip/num ；num 网络号位数
- 公有 IP 
- 私有 IP ：.255 为广播地址  .0 为网络地址
  - 10.0.0.0 - 10.255.255.255          A 类
  - 172.16.0.0 - 172.31.255.255      B 类
  - 192.168.0.0 - 192.168.255.255  C 类
- ip 有定位功能，导航功能
- MAC 通信范围小，子网内
- MTU 1500 不包含头 14 B 和尾部 4 B
- scope global 对外 / host 本机，内核处理后返回
- qdisc 排队规则，pfifo_fast 有优先级的 fifo ，由 ip 头的 TOS 指定优先级

```shell
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:0c:29:ae:88:49 brd ff:ff:ff:ff:ff:ff
    inet 192.168.153.129/24 brd 192.168.153.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::20c:29ff:feae:8849/64 scope link 
       valid_lft forever preferred_lft forever
```

#### 4. DHCP PXE

- 添加 IP 地址

  ```shell
  $ sudo ip addr add 10.0.0.1/24 dev eth1
  $ sudo ip link set up eth1
  ```

- 若是同网段，发送 ARP 来请求 MAC 地址；不同网段，则向网关发送 ARP 请求

- DHCP 动态主机配置，基于 UDP 和 BOOTP ，是 BOOTP 的增强版，分为四个步骤：

  - DHCP Discover ：广播 MAC + 本机 MAC ：ALL 0 IP + ALL 255 IP ：源 port 68 + 目的 port 67 ：本机 MAC + 请求 IP
  - DHCP Offer ：广播 MAC + 本机 MAC ：本机 IP + ALL 255 IP ：源 port 67 + 目的 port 68 ：目的 MAC + offer IP（ 可能收到多个 Offer ）
  - DHCP Request ：广播接收第一个 Offer ，并拒绝其他 Offer。
  - DHCP Ack ：指定租期

- 租期：过 50% 可以重发 DHCP Request 续约

- PXE 预启动执行环境，自动安装操作系统

  - OS 启动 BIOS -》 MBR 启动扇区 -》GRUB -》加载内核 initramfs -》内核
  - 客户端放在 BIOS 中，通过 DHCP 获取 IP；通过 DHCP 回复中执行 next-server 得到 PXE 服务器 IP 以及启动文件名 filename 
  - 通过 TFTP 协议下载文件

#### 5. LAN 

- 网线直连 ：1 2 线 收，3 6 线 发；交换 1 3 和 2 6 

  网线一端的第 1 脚连另一端的第 3 脚，网线一端的第 2 脚连另一头的第 6 脚，其他脚一一对应即可。 这种排列做出来的通常称之为“交叉线”。

- hub 集线器，无脑广播，复制到其他端口

- MAC 帧格式 ：目的 MAC 6 B + 源 MAC 6 B + 类型 2 B ( IP / ARP ) + 数据 + CRC 4 B

- ARP 缓存

- 交换机：学习 MAC 地址与网口的对应关系，建立转发表，但有过期时间

- 问 1：RARP 作用，通过 MAC 获取 IP 地址，局域网管理员指定机器 IP ，在 RARP 服务器上配置

- 问 2：ARP 遇多个交换机有什么问题，有环路时会不断广播形成广播风暴

#### 6. 交换机

- 环路问题：主机 ARP 广播后，交换机学习主机的位置，然后继续广播，造成学习到的主机端口位置不断变化
- 图 -》 破环 -》树 -》最小生成树
- STP Spanning Tree Protocol ；缺点，大网络中，网络改变后要重新收敛
  - Root Bridge 根交换机
  - Designated Bridge 指定交换机
  - Bridge Protocol Data Units BPDU 网桥协议数据单元
  - Priority Vector 优先级向量 [Root Bridge ID, Root Path Cos, Bridge ID, Port ID]
  - 通过比较优先级向量来归顺/收复其他交换机
- 解决广播/安全问题
  - 物理隔离：交换机 + router
  - 虚拟隔离：VLAN 802.11 Q tag 包含 VLAN ID
    - 交换机口，每个口属于一个 VLAN ，相同的 VLAN 才会互相转发
    - Trunk ：转发所有的 VLAN 包，可以用于交换机间互联

#### 7. ICMP

- ICMP 网络控制报文协议，基于 IP 封装
- 报文类型 ：主动请求 -》8；主动请求的应答 -》0
- 查询报文：ping 主动请求 多了 标识符和序号，在数据中包含发送请求的时间
  - ICMP Echo Req 
  - ICMP Echo Reply
- 差错报文：
  - 终点不可达 3  不可达原因：网络不可达 0，主机不可达 1 ，协议不可达 2，端口不可达 3 ，需分片但不允许 4 
  - 源抑制 4
  - 超时 11
  - 重定向 5
- traceroute 
  - 设置了 TTL 的 UDP 包，选择一个不可能的 UDP 端口号，大于 30000，会返回端口不可达的错误报文
  - 设置不分片，可以确定路径中的 MTU

#### 8. 网关

- 静态路由
- 通过网关 MAC 都要变
- 过网关不改变 IP -》转发网关，在 IP 不冲突时
- 过网关改变 IP -》NAT，IP冲突

#### 9. 路由

- 目标网络，出口设备，下一跳网关，使用 route or ip route 查路由表
- 添加路由项 `ip route add 10.176.48.0/20 via 10.173.32.1 dev eth0`
- 策略路由：
  - 可以配置多个路由表，可以根据源 IP 地址、入口设备、TOS 等选择路由表，然后再路由表中查找路由
  - 在一条路由规则中，也可以走多条路径。进行权重分配
- 动态路由算法：
  - RIP 距离矢量路由，基于 Bellman-Ford 算法，与邻居分享路由；好消息(新节点)传得快，坏消息(节点 down)传得慢；要发送所有的路由信息，适用于小网路 < 15 跳。
  - OSPF 链路状态路由，基于 Dijkstra 算法，首先测试与邻居节点的距离，然后将此信息广播出去，这样每个节点都能构建一个完整的图，然后使用 Dijkstra 算法找到最短路径。多个路径能实现负载均衡。
  - RIP OSPF 用于内网；
  - 外网路由协议 BGP  路径矢量路由协议，链路中途路由的升级版
    - eBGP：自治系统间，边界路由器之间使用 eBGP 
    - iBGP ：自治系统内部

#### 10. UDP

- 建立连接：维护连接的数据结构
- TCP 面向连接，提供可靠交付，面向字节流，拥塞控制，有状态服务
- 应用：DHCP，TFTP，IGMP(多播) VXLAN 
- 应用层封装：
  - 网页 or APP 访问，原来是 http (基于 TCP)，QUIC 快速 UDP 互联网连接
  - 流媒体，直播 RTMP(基于 TCP)，UDP
  - 实时游戏，TCP 需要维护数据结构，再 async IO 出现之前，使用 UDP
  - IoT，Thread Group 物联网通信协议，基于 UDP
  - 移动通信，GTP-U 基于 UDP 协议

#### 11. TCP-1

- 解决：顺序，丢包，连接维护，流量控制，拥塞控制
- 三次握手，两人都单方面有去有回，客户端一般会立即发送数据
- keep-alive
- 序号不能都从 1 开始，与三次握手理由一致
- tcp_fin_timeout 主动关闭的一方二次挥手后处于等待状态，TCP 协议没有对等待超时进行规定，Linux 则可以通过 tcp_fin_timeout 设置
- time_wait 保证第四次握手被接收，2MSL 最大报文生存时间，TTL

#### 12. TCP-2

- 累积应答，接收窗口大小 = 接收 buffer 大小 - 缓存占用大小

- 超时时间 > RTT 通过采样自适应调整，超时后超时时间加倍

- 快速重传：当接收方接收到一个序号大于下一个所期望的报文段时，发送三个冗余的 ACK ，接收到 ACK 后马上重发

- SACK ，将缓存的地图发给发送方，使其判断出有那些包欠缺

- 流量控制，窗口太小不更新窗口，待大到一定数值再开放，避免 buffer 马上又被填满

- 拥塞控制，LastByteSent -LastByteAcked <= min{ cwnd, rwnd } 拥塞窗口和流量控制的滑动窗口

  理想情况，通道容量 = 带宽 x 往返延迟；避免包丢失和重传

  cwnd 从 1 指数增长，当 cwnd > ssthresh (65535) ，之后没收到一个确认，cwnd 增加 1/cwnd

  出现拥塞时，需要重传 ssthresh 设为 cwnd/2 将 cwnd 设为 1 重新开始慢启动

  使用快速重传算法时，cwnd 设为 cwnd / 2， ssthresh = cwnd ，收到三个 ACK ，cwnd = ssthresh + 3；

  问题：1. 丢包不代表通道满了；2. 会填满缓存，导致延时大；

- BBR 拥塞算法

  - 不断加快发送速度，将管道填满，但不降中间设备缓存填满