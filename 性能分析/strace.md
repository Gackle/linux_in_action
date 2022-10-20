---
description: strace 命令 —— 用于诊断、调试和教学的 Linux 用户空间跟踪器
---
# strace 命令

按照 strace 官网的描述， `strace` 是一个可用于诊断、调试和教学的 Linux 用户空间跟踪器。我们用它来监控用户空间进程和内核的交互，比如系统调用、信号传递、进程状态变更等。

**strace** 底层使用内核的 `ptrace` 特性来实现其功能。

在运维的日常工作中，故障处理和问题诊断是个主要的内容，也是必备的技能。 **strace** 作为一种动态跟踪工具，能够帮助运维高效地定位进程和服务故障。它像是一个侦探，通过系统调用的蛛丝马迹，告诉你异常的真相。

## P.S. 系统调用

在计算机中，**系统调用**(*system call*)，又称为系统呼叫，指运行在用户空间的程序向操作系统内核请求需要更高权限运行的服务。

系统调用提供用户程序与操作系统之间的接口。操作系统的进程空间分为 用户空间 和 内核空间 ：

 - 操作系统内核直接运行在硬件上，提供设备管理、内存管理、任务调度等功能。
 - 用户空间通过 API 请求内核空间的服务来完成其功能 ———— 内核提供给用户空间的这些 API , 就是系统调用。

在Linux系统上，应用代码通过 `glibc` 库封装的函数，间接使用系统调用。

Linux内核目前有300多个系统调用，详细的列表可以通过 *syscalls* 手册页查看。这些系统调用主要分为几类：

 - 文件和设备访问类 比如 `open`/`close`/`read`/`write`/`chmod` 等
 - 进程管理类 `fork`/`clone`/`execve`/`exit`/`getpid` 等
 - 信号类 `signal`/`sigaction`/`kill` 等
 - 内存管理 `brk`/`mmap`/`mlock等`
 - 进程间通信IPC `shmget`/`semget` * 信号量，共享内存，消息队列等
 - 网络通信 `socket`/`connect`/`sendto`/`sendmsg` 等
 - 其他

常见的系统调用功能描述

| 系统调用 | 作用 |
|:---|:---|
|read|从一个文件描述符（文件，socket）读取字节|
|write|向一个文件描述符（文件，socket）写入字节|
|open|打开一个文件（返回一个文件描述符）|
|close|关闭一个文件描述符|
|fork|创建一个新进程（当前进程被分叉）|
|exec|执行一个新程序|
|connect|连接到一个网络主机|
|accept|接受一个网络连接|
|stat|读取文件统计信息|
|ioctl|设置 I/O 属性，或其它杂项函数|
|mmap|将一个文件映射到进程内存地址空间|
|brk| 扩展堆指针 |


## 命令用法 + 参数说明

``` shell
$ strace -h
usage: strace [-CdffhiqrtttTvVwxxy] [-I n] [-e expr]...
              [-a column] [-o file] [-s strsize] [-P path]...
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]
   or: strace -c[dfw] [-I n] [-e expr]... [-O overhead] [-S sortby]
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]

Output format: # 输出格式
  -a column      alignment COLUMN for printing syscall results (default 40)
  -i             print instruction pointer at time of syscall
  -k             obtain stack trace between each syscall (experimental)
  -o file        send trace output to FILE instead of stderr
  -q             suppress messages about attaching, detaching, etc.
  -r             print relative timestamp
  -s strsize     limit length of print strings to STRSIZE chars (default 32)
  -t             print absolute timestamp
  -tt            print absolute timestamp with usecs
  -T             print time spent in each syscall
  -x             print non-ascii strings in hex
  -xx            print all strings in hex
  -y             print paths associated with file descriptor arguments
  -yy            print protocol specific information associated with socket file descriptors

Statistics:  # 统计项
  -c             count time, calls, and errors for each syscall and report summary
  -C             like -c but also print regular output
  -O overhead    set overhead for tracing syscalls to OVERHEAD usecs
  -S sortby      sort syscall counts by: time, calls, name, nothing (default time)
  -w             summarise syscall latency (default is system time)

Filtering:  # 过滤项
  -e expr        a qualifying expression: option=[!]all or option=[!]val1[,val2]...
     options:    trace, abbrev, verbose, raw, signal, read, write, fault
  -P path        trace accesses to path

Tracing:  # 跟踪项
  -b execve      detach on execve syscall
  -D             run tracer process as a detached grandchild, not as parent
  -f             follow forks
  -ff            follow forks with output into separate files
  -I interruptible
     1:          no signals are blocked
     2:          fatal signals are blocked while decoding syscall (default)
     3:          fatal signals are always blocked (default if '-o FILE PROG')
     4:          fatal signals and SIGTSTP (^Z) are always blocked
                 (useful to make 'strace -o FILE PROG' not stop on ^Z)

Startup:  # 启动项
  -E var         remove var from the environment for command
  -E var=val     put var=val in the environment for command
  -p pid         trace process with process id PID, may be repeated
  -u username    run command as username handling setuid and/or setgid

Miscellaneous:  # misc 其他
  -d             enable debug output to stderr
  -v             verbose mode: print unabbreviated argv, stat, termios, etc. args
  -h             print help message
  -V             print version
```

其中 `PROG` 是要诊断的程序的路径

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -c | 统计每一个系统调用所执行的时间、次数和出错的次数 |
| -d | 显示有关标准错误的 strace 本身的一些调试输出 |
| -f | 跟踪子进程，这些子进程是由于 `fork(2)` 系统调用而由当前跟踪的进程创建的 |
| -i | 在系统调用时打印指令指针 |
| -t | 跟踪的每一行都以时间为前缀 |
| -tt | 如果输入两次，则打印的时间将精确至微秒 |
| -T | 显示花费在系统调用上的时间。这将记录每个系统调用的开始和结束之间的时间差 |
| -v | 打印环境，统计信息，termios等调用的未缩写版本。这些结构在调用中非常常见，因此默认行为显示了结构成员的合理子集。使用此选项可获取所有详细信息 |
| -e expr | 限定表达式，用于修改要跟踪的事件或如何跟踪它们，可用的选项有 **trace, abbrev, verbose, raw, signal, read, write, fault** |
| -o 文件名 | 将跟踪输出写入文件名而不是stderr |
| -p pid | 使用进程ID pid附加到该进程并开始跟踪。跟踪可以随时通过键盘中断信号（CTRL -C）终止 |
| -S | 按指定条件对-c选项打印的直方图输出进行排序 |
| -u username | 以 username 的 UID 和 GID 执行被跟踪的命令 |


### 针对 -e trace 的特别说明

要跟踪某个具体的系统调用，`-e trace=xxx` 即可。但有时候我们要跟踪一类系统调用，比如所有和文件名有关的调用、所有和内存分配有关的调用。

如果人工输入每一个具体的系统调用名称，可能容易遗漏。于是 strace 提供了几类常用的系统调用组合名字

* `-e trace=file` —— 跟踪和文件访问相关的调用(参数中有文件名)
* `-e trace=process` —— 跟踪涉及过程管理的所有系统调用，比如 `fork`/`exec`/`exit_group` 。 这对于观察进程的派生，等待和执行步骤很有用
* `-e trace=network` —— 跟踪所有与网络相关的系统调用，比如 `socket`/`sendto`/`connect`
* `-e trace=signal` —— 跟踪所有与信号相关的系统调用，比如 `kill`/`sigaction`
* `-e trace=desc` —— 跟踪和文件描述符相关的系统调用，比如 `write`/`read`/`select`/`epoll`
* `-e trace=ipc` —— 跟踪所有与 IPC 相关的系统调用，比如 `shmget` 

## 使用示例

1. 跟踪nginx, 看其启动时都访问了哪些文件

```shell
$ strace -tt -T -f -e trace=file -o /data/log/strace.log -s 1024 ./nginx
```

2. 定位一次系统无法解析域名故障
   已排除DNS解析失败，域名解析通常跟系统读取文件相关

```shell
$ strace -e strace=open ping www.baidu.com
```

3. 定位进程异常退出
   机器上有个叫做 run.sh 的常驻脚本，运行一分钟后会死掉；假设运行的 PID 是 24298

```shell
$ strace -o strace.log -tt -p 24298
```
