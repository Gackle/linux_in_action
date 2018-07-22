---
description: netstat 命令 —— 用于显示网络连接状态、路由表信息、接口的统计数据、伪装连接、多播成员关系等
---

# netstat 命令

`netstat` 命令用来打印 Linux 中网络系统的状态信息，可让你得知整个 Linux 系统的网络情况。

它可以
1. 显示路由表，实际的网络连接以及每一个网络接口设备的状态信息
2. 显示与 IP, TCP, UDP 和 ICMP 协议相关的统计数据，一般用于查询本机各端口的网络连接情况

## 命令用法

``` shell
$ NETSTAT [-a] [-b] [-e] [-f] [-n] [-o] [-p] [-r] [-s] [-x] [-t] [interval][--ip]
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -a, -all | 显示所有连接和侦听端口（默认显示已连接的端口信息 |
| -e | 显示以太网的统计信息。可与 `-s` 结合使用 |
| -n | 直接使用 ip 地址，而不通过域名服务器 |
| -r | 显示路由表信息 |
| -s | 显示网络工作信息统计表。默认情况下，显示 IP、IPv6、ICMP、ICMPv6、TCP、TCPv6、UDP 和 UDPv6 的统计信息 |
| -p | 显示与每个连接相关的所属进程的 PID/ 进程名 |
| -l | 显示正在监听的端口信息 |

## 结果参数解析

``` shell
gackle@machine:~$ netstat -p
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
...
Active UNIX domain sockets (w/o servers)
Proto RefCnt Flags       Type       State         I-Node   Path
...
```

其中分为两部分：
1. **Active Internet connections**，称为**有源TCP连接**，其中 `Recv-Q` 和 `Send-Q` 指的是接收队列和发送队列。这些数字一般都应该是0。如果不是则表示软件包正在队列中堆积。这种情况只能在非常少的情况见到。其他如 `Local Address` 以及 `Foreign Address` 分别代表本地地址信息和外部地址信息，`State` 代表连接的状态。

2. **Active UNIX domain sockets**，称为**有源 Unix 域套接字**（和网络套接字一样，但只用于本机通信，性能提高一倍）。其中 `RefCnt` 代表连接到本套接字上的进程号，`Type` 表示套接字的类型，`State` 显示套接字连接状态，`Path` 表示连接到套接字的其它进程使用的路径名

其中关于连接状态 `State` 的值有：

| 值 | 含义 |
|:---|:---|
| LISTEN | 监听来自远方的TCP端口的连接请求 |
| SYN-SENT | 在发送连接请求后等待匹配的连接请求 |
| SYN-RECEIVED | 在收到和发送一个连接请求后等待对方对连接请求的确认 |
| ESTABLISHED | 代表一个打开的连接 |
| TIME-WAIT | 等待足够的时间以确保远程TCP接收到连接中断请求的确认 |
| CLOSED | 没有任何连接状态 |
| CLOSED-WAIT | 等待从本地用户发来的连接中断请求 |

## 使用实例

1. 查看端口占用
    ``` bash
    #查看8090 端口占用情况
    $ netstat -nlp | grep 8090
    ```
2. 实现网络设备列表
    ``` bash
    $ netstat -i
    Kernel Interface table
    Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
    eth0      1500        0      0      0 0             0      0      0      0 BMRU
    eth1      1500        0      0      0 0             0      0      0      0 BMRU
    eth2      1500        0      0      0 0             0      0      0      0 BMRU
    lo        1500        0      0      0 0             0      0      0      0 LRU
    wifi0     1500        0      0      0 0             0      0      0      0 BMRU
    ```
3. 查找程序运行的端口
    ``` bash
    $ netstat -anp | grep './server'
    ```
4. 显示路由表信息
    ``` bash
    Kernel IP routing table
    Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
    link-local      0.0.0.0         255.255.0.0     U         0 0          0 eth0
    169.254.134.81  0.0.0.0         255.255.255.255 U         0 0          0 eth0
    169.254.255.255 0.0.0.0         255.255.255.255 U         0 0          0 eth0
    224.0.0.0       0.0.0.0         240.0.0.0       U         0 0          0 eth0
    255.255.255.255 0.0.0.0         255.255.255.255 U         0 0          0 eth0
    192.168.56.0    0.0.0.0         255.255.255.0   U         0 0          0 eth1
    ...
    255.255.255.255 0.0.0.0         255.255.255.255 U         0 0          0 wifi0
    ```