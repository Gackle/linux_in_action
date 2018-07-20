---
description: ifconfig 命令 —— 配置和显示Linux内核中网络接口的网络参数
---

# ifconfig 命令

在 Linux 中 `ifconfig` 命令用于显示或设置网络设备。
`ifconfig` 可设置网络设备的状态，或是显示目前的设置。

## 命令用法

``` shell
ifconfig [-a] [-v] [-s] <interface> [[<AF>] <address>]
  [add <address>[/<prefixlen>]]
  [del <address>[/<prefixlen>]]
  [[-]broadcast [<address>]]  [[-]pointopoint [<address>]]
  [netmask <address>]  [dstaddr <address>]  [tunnel <address>]
  [outfill <NN>] [keepalive <NN>]
  [hw <HW> <address>]  [mtu <NN>]
  [[-]trailers]  [[-]arp]  [[-]allmulti]
  [multicast]  [[-]promisc]
  [mem_start <NN>]  [io_addr <NN>]  [irq <NN>]  [media <type>]
  [txqueuelen <NN>]
  [[-]dynamic]
  [up|down] ...
```

其中：
- `interface` 指定的网络设备名称
- `add <address>` 设置网络设备的 IPv6 地址
- `del <address>` 删除网络设备的 IPv6 地址
- `up` 启动指定的网络设备
- `down` 关闭指定的网络设备
- `netmask <address>` 指定网络设备的子网掩码地址
- `[<AF>] <address>` 指定网络设备的 IP 地址，可配合地址簇使用
- `<AF>` 指定的地址簇，默认是 *inet*，常用的可选地址簇如下：
    - *unix* Unix 域
    - *inet* DARPA 网络
    - *inet6* IPv6 地址
    - *ipx* Novell IPX
    - *ddp* Appletalk DDP
- `<hw <HW> <address>` 指定网络设备的类型 HW 与硬件地址 address。
- `<HW>` 指定的设备硬件类型，常用的可选类型如下：
    - *loop* 本地回环 loopback 端口
    - *ether* 以太网
    - *ppp* 点对点协议


## 参数解析

``` shell
gackle@machine:~$ ifconfig

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 169.254.134.81  netmask 255.255.0.0  broadcast 169.254.255.255
        inet6 fe80::985a:92ed:f689:8651  prefixlen 64  scopeid 0x0<global>
        ether 02:00:4c:4f:4f:50  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.1  netmask 255.255.255.0  broadcast 192.168.56.255
        inet6 fe80::1028:113f:f3b7:ffed  prefixlen 64  scopeid 0x0<global>
        ether 0a:00:27:00:00:10  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
...
```

其中：

- `eth0`: 网络设备名，其中常见的还有 `lo` 回环地址
- `flags`: `UP`（代表网卡开启状态）`RUNNING`（代表网卡的网线被接上）`MULTICAST`（支持组播）`MTU:1500`（最大传输单元：1500字节）
- `inet`：IPv4 地址
- `netmask`：IPv4 的子网掩码
- `broadcast`：IPv4 的广播地址
- `ether`：网络设备的 MAC 地址
- `inet6`：IPv6 的地址
- `RX packets 0  bytes 0 (0.0 B)`：接收数据包以及字节数
- `TX packets 0  bytes 0 (0.0 B)`：发送数据包以及字节数

## 使用实例
1. 设置 IP 地址和掩码
    ``` shell
    $ ifconfig eth0 192.168.5.40 netmask 255.255.255.0
    ```
2. 修改 MAC 地址
    ``` shell
    $ ifconfig eth0 down
    $ ifconfig eth0 hw ether 00:AA:BB:CC:DD:EE
    $ ifconfig eth0 up
    $ ifconfig eth1 hw ether 00:1D:1C:1D:1E
    $ ifconfig eth1 up
    ```
3. 设置最大传输单元
    ``` shell
    $ ifconfig eth0 mtu 1500 
    ```