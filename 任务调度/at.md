---
description: at 命令 —— 定时执行 Linux 任务
---
# at 命令

`at` 命令用于在一个指定的时间执行一个指定任务，只能执行一次，且需要开启 atd 进程。

`at` 命令会将作业提交到队列中，指定shell何时运行该作业。`at` 的守护进程 atd 会以后台模式运行，检查作业队列来运行作业。

在你使用 `at` 命令时，该作业会被提交到作业队列（job queue）。作业队列会保存通过 `at` 命令提交的待处理的作业。针对不同优先级，存在 26 种不同的作业队列。作业队列通常用小写字母 `a~z` 和大写字母 `A~Z` 来指代。

> <u>`at` 命令运行原理</u>
> 
> atd 守护进程会检查系统上的一个特殊目录（通常位于 **/var/spool/at** ）来获取用 `at` 命令提交的作业。默认情况下，atd 守护进程会每 60 秒检查一下这个目录。有作业时，atd 守护进程会检查作业设置运行的时间。如果时间跟当前时间匹配，atd 守护进程就会运行此作业。 


## 关于 atd 进程

要使用一次性计划任务时，我们的 Linux 系统上面必须要有负责这个计划任务的服务，那就是 atd 服务。 不过并非所有的 Linux 发行版都默认会把他打开的，所以，某些时刻我们需要手动将atd 服务激活才行。

1. 查看 atd 进程是否开启
    ``` bash
    gackle@machine:~$ ps -ef | grep atd
    gackle     32     4  0 19:30 tty1     00:00:00 grep atd
    ```
2. 开启 atd 进程
    ``` bash
    gackle@machine:~$ /etc/init.d/atd start
    # 或者
    gackle@machine:~$ /etc/init.d/atd restart
    ```
3. 开机即运行 atd 进程
    ``` bash
    gackle@machine:~$ chkconfig –level 2345 atd on
    ```

## 命令用法

``` shell
$ at [options] time
```

### time 格式参数 
`at` 命令能识别多种不同的时间格式。

- 标准的小时和分钟格式，比如10:15。
- AM/PM指示符，比如10:15 PM。
- 特定可命名时间，比如 now、noon、midnight 或者 teatime（4 PM）。 除了指定运行作业的时间，也可以通过不同的日期格式指定特定的日期。 
- 标准日期格式，比如 MMDDYY、MM/DD/YY 或 DD.MM.YY。
- 文本日期，比如 Jul 4 或 Dec 25，加不加年份均可。
- 你也可以指定时间增量。
    - 当前时间 + 25 min: now + 25 min
    - 明天 10:15 PM: 10:15 + 1days / 10:15 tomorrow
    - 10:15+7天: 10:15 + 7days
    
 

## 常用可选参数 

| 参数 | 说明 |
|:---|:---|
| -c |打印任务的内容到标准输出 |
| -f | 从指定文件读入任务，而不是从 stdin 读入 |
| -q | 指定系任务的队列名称 |
| -l | 显示待执行任务的列表 |
| -d | 删除指定的待执行任务 |
| -t | 以时间参数的形式提交
| -m | 任务执行完成后向用户发送 Email |
| -v | 显示任务将被执行的时间 |
| -I | atq 的别名 |
| -d | atrm 的别名 |

## 使用实例

1. 明天 17 点钟，输出时间到指定文件内
    ``` shell
    $ at 17:00 tomorrow
    at> date>/tmp/date.log
    at> <Ctrl+D>
    ```
2. 查看系统没有执行的工作任务
    ``` shell
    $ atq
    3       Sun Jul 22 10:15:00 2018 a gackle
    4       Sat Jul 21 20:53:00 2018 a gackle
    ```
3. 删除已经设定的任务
    ``` shell
    $ atrm 3
    $ atq
    4       Sat Jul 21 20:53:00 2018 a gackle
    ```
4. 查看任务内容
    ``` bash
    $ at -c 3
    at -c 3
    #!/bin/sh
    # atrun uid=1000 gid=1000
    # mail gackle 0
    umask 0
    ...
    /bin/ls
    ```