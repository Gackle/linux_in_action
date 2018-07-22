---
description: route 命令 —— 
---

# route 命令

`route` 命令用来显示并设置 Linux 内核中的网络路由表，`route` 命令设置的路由主要是静态路由。显示路由的效果和 `netstat -r` 等同。

在 Linux 系统中设置路由通常是为了解决以下问题：<u>该 Linux 系统在一个局域网中，局域网中有一个网关，能够让机器访问Internet，那么就需要将这台机器的 ip 地址设置为 Linux 机器的默认路由</u>。

## 命令用法 

``` bash
# 显示系统内核路由表
route [-nNvee] [-FC] [<AF>] 

# 修改指定路由表信息
route [-v] [-FC] {add|del|flush} ...  
```

其中：
`<AF>` 可以使用 `-4`、`-6`、`'-A <af>` 或 `--<af>` 来表示，默认是 `inet`，`<af>` 的取值为 ：

- inet (DARPA Internet)
- inet6 (IPv6)
- ax25 (AMPR AX.25)
- netrom (AMPR NET/ROM)
- ipx (Novell IPX)
- ddp (Appletalk DDP)
- x25 (CCITT X.25)

## 常用可选参数 

| 参数 | 说明 |
|:---|:---|
| -n, --numeric | 不执行 DNS 反向查找，直接显示数字形式的 IP 地址 |
| -e, --extend | 以 `netstat` 命令格式显示路由表 |
| -v, --verbose | 显示详细信息 |



## 结果参数解析

``` shell
gackle@machine:~$ route
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
link-local      0.0.0.0         255.255.0.0     U     256    0        0 eth0
...
```

其中：
- Destination： 目标地址
- Gateway： 网关地址
- Genmask： 子网掩码
- Flags： 路由标识，标记当前网络节点的状态：
    - U Up表示此路由当前为启动状态。
    - H Host，表示此网关为一主机。
    - G Gateway，表示此网关为一路由器。
    - R Reinstate Route，使用动态路由重新初始化的路由。
    - D Dynamically,此路由是动态性地写入。
    - M Modified，此路由是由路由守护程序或导向器动态修改。
    - ! 表示此路由当前为关闭状态。

## 使用实例

1. 设置网关/添加网关
    ``` bash
    #增加一条到达 244.0.0.0 的路由
    $ route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0    
    ```
2. 屏蔽路由
    ``` bash
    #增加一条屏蔽的路由，目的地址为 224.x.x.x 将被拒绝
    $ route add -net 224.0.0.0 netmask 240.0.0.0 reject
    ```
3. 删除路由记录
    ``` bash
    $ route del -net 224.0.0.0 netmask 240.0.0.0
    $ route del -net 224.0.0.0 netmask 240.0.0.0 reject
    ```