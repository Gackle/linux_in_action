---
description: ps 命令 —— 监控进程
---

# ps 命令 #

当程序运行在系统上时，我们称之为**进程（process）**。监控进程我们可以使用 `ps` 命令，它能输出运行在系统上的所有程序的许多信息。

``` bash
gackle@machine:~$ ps
  PID TTY          TIME CMD
    4 tty1     00:00:00 bash
   17 tty1     00:00:00 ps
```

默认情况下，`ps` 命令只会显示运行在当前控制台下的属于当前用户的进程。

> 由于 `ps` 命令曾经有两个版本，因此有多个命令行参数集（控制输出什么信息并如何显示），同时也支持三种风格的参数形式（Unix、BSD 以及 GNU 风格），由于实在太多太复杂，所以我们只需要记住我们常用的参数即可。

## 常用参数列表 ##

| 参数 | 说明 | 风格 |
|:---|:---|:---:|
| -C cmdlist | 显示包含在 cmdlist 列表中的进程 | Unix 风格 |
| -G grplist | 显示 组ID 在 grplist 列表中的进程 | Unix 风格 |
| -U userlist | 显示 属主的用户ID 在 userlist 列表中的进程 | Unix 风格 |
| -p pidlist | 显示 PID 在 pidlist 列表中的进程 | Unix 风格 |
| -t ttylist | 显示 终端ID 在 ttylist 列表中的进程 | Unix 风格 |
| -u userlist | 显示有效用户ID在 userlist 列表中的进程 | Unix 风格 |
| -l | 显示长列表 | Unix 风格|
| -e/-A | 显示所有进程 | Unix 风格| 
| -f | 显示完整格式的输出 | Unix 风格|
| e | 显示命令使用的环境变量 | BSD 风格 |
| m | 在进程后显示线程 | BSD 风格 |
| --forest | 用层级结构显示出进程和父进程之间的关系 | GNU 风格 |


## 结果解析 ##

这里我们用使用 `ps -l` 以及 `ps l` 来打印长列表，同时解析表头参数含义：

``` shell
# Unix 风格
gackle@machine:~$ ps -l
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000     4     3  0  80   0 -  3442 -      tty1     00:00:00 bash
0 R  1000    16     4  0  80   0 -  3759 -      tty1     00:00:00 ps

# BSD 风格
gackle@machine:~$ ps l
F   UID   PID  PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
0  1000     4     3  20   0  13772  2088 -      S    tty1       0:00 -bash
0  1000    31     4  20   0  15036  1668 -      R    tty1       0:00 ps l
```

| 列名 | 含义 |
|:---|:---|
| F | 内核分配给进程的系统标记 |
| S | 进程的状态（O 代表正在运行；S 代表休眠；R 代表可运行正等待；Z 代表僵化，进程已结束但父进程不存在；T 代表停止） |
| UID | 启动这些进程的用户 |
| PID | 进程的进程 ID |
| PPID | 父进程的进程号（如果该进程是由另一个进程启动的）|
| C | 进程生命周期中的 CPU 利用率 |
| PRI | 进程的优先级（数字越大代表优先级越小） |
| NI | 谦让度值用来参与决定优先级 |
| ADDR | 进程的内存地址 |
| SZ | 假如进程被换出，所需交换空间的大致大小 |
| WCHAN | 进程休眠的内核函数的地址 |
| TTY | 进程启动时的终端设备 |
| TIME | 运行进程需要的累计 CPU 时间 |
| CMD | 启动的程序的名称 |
| --- | -- BSD 风格参数额外信息 -- |
| VSZ | 进程在内存中的大小，以千字节（KB）为单位 |
| RSS | 进程在未换出时占用的物理内存 |
| STAT | 代表当前进程状态的双字符状态码（第一个字符和 S 列一样，第二个字符进一步说明进程的状态：\< 运行在高优先级上；N 运行在低优先级上；L 有页面锁定在内存中；s 该进程是控制进程；l 该进程是多线程的） |