---
description: uptime 命令 —— 显示系统已经运行了多久 
---

# uptime 命令

`uptime` 命令能够打印系统总共运行了多长时间和系统的平均负载。

## 命令用法

``` shell
$ uptime [options]
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -p, --pretty | 以更好的格式显示数据 |
| -s, --since | 显示系统启动时间 |

## 结果参数解析

``` bash
gackle@machine:~$ uptime
 17:43:55 up  2:53,  0 users,  load average: 0.52, 0.58, 0.59
```

`uptime` 命令可以显示的信息显示依次为：

- 当前时间
- 系统已经运行了多长时间
- 目前有多少登陆用户
- 系统在过去的 1 分钟、5 分钟和 15 分钟内的平均负载

---

``` bash 
gackle@machine:~$ uptime -s
2018-07-18 14:50:04
```

显示系统的启动时间。

## 平均负载
<big><font color="lightblue">系统平均负载是指在特定时间间隔内运行队列中的平均进程数。</font></big>

如果每个 CPU 内核的当前活动进程数不大于 3 的话，那么系统的性能是良好的。如果每个CPU内核的任务数大于 5，那么这台机器的性能有严重问题。

如果你的 Linux 主机是 1 个双核CPU的话，当 Load Average 为 6 的时候说明机器已经被充分使用了。