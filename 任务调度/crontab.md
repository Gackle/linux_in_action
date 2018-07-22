---
description: crontab 命令 —— 初始化用户的 crontable 文件对应的编辑器（如果允许的话） 
---

Linux 系统使用 `cron` 程序来安排要定期执行的作业。`cron` 程序会在后台运行并检查一个特殊的表（被称作 cron 时间表），以获知已安排执行的作业。 

# cron 时间表

cron 时间表采用一种特别的格式来指定作业何时运行。其格式如下： 

    min hour dayofmonth month dayofweek command 

cron 时间表允许你用特定值、取值范围（比如 1~5 ）或者是通配符（`*`）来指定条目。例如，如果想在每天的 10:15 运行一个命令，可以用 cron 时间表条目： 

    15 10 * * * command 

<u>在 cron 时间表里，每一行都代表一项任务，每行的每个字段代表一项设置</u>。

# crontab 命令 —— 构建 cron 时间表

每个系统用户（包括root用户）都可以用自己的 cron 时间表来运行安排好的任务。Linux提供了 `crontab` 命令来处理 cron 时间表。

`crontab` 命令被用来提交和管理用户的需要周期性执行的任务，与 Windows 下的计划任务类似，当安装完成操作系统后，默认会安装此服务工具，并且会自动启动 crond 进程，crond 进程每分钟会定期检查是否有要执行的任务，如果有要执行的任务，则自动执行该任务。

## 命令用法

``` shell
$ crontab [-u user] file
# 或者 
$ crontab [ -u user ] [ -i ] { -e | -l | -r }
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -e | 编辑该用户的 cron 时间表设置 |
| -l | 列出该用户的 cron 时间表设置 |
| -r | 删除该用户的 cron 时间表设置 | 
| -u user | 指定要设定 cron 时间表的用户名称 | 

## 使用实例 

0. 列出已有的 cron 时间表：
    ``` shell
    $ crontab -l
    
    # 添加 cron 时间表
    $ crontab -e
    <第一次选择编辑器，然后键入配置>
    ```
1. 每分钟执行一次 ls 命令
    ```
    * * * * * ls
    ```
2. 在上午8点到11点的第3和第15分钟执行
    ```
    3,15 8-11 * * * COMMAND
    ```
3. 晚上11点到早上7点之间，每隔一小时重启smb
    ```
    * 23-7/1 * * * /etc/init.d/smb restart
    ```
4. 每个星期一的上午8点到11点的第3和第15分钟执行
    ```
    3,15 8-11 * * 1 command
    ```
5. 每个月的最后一天执行的命令
    ```
    00 12 * * * if [`date +%d -d tomorrow` = 01 ] ; then ; command
    ```

如果你创建的脚本对精确的执行时间要求不高，用预配置的 cron 脚本目录会更方便。有 4 个基本目录：<u>hourly、daily、monthly 和 weekly</u>。 

``` bash
gackle@machine:~$ ls /etc/cron.*ly
/etc/cron.daily:
apt-compat  bsdmainutils  dpkg  exim4-base  logrotate  man-db  mlocate  passwd

/etc/cron.hourly:

/etc/cron.monthly:

/etc/cron.weekly:
man-db
```

因此如果脚本需要每天运行一次，只要将脚本复制到 daily 目录，cron 就会每天执行它。 

# crond 服务

大多数情况下，设置了 cron 时间表但是没有执行，通常是因为 crond 服务没有运行。我们可以用以下命令来解决：

``` shell
# 查看 crond 服务状态
$ service crond status

# 启动 crond 服务
$ /sbin/service crond start

# 关闭 crond 服务
$ /sbin/service crond stop

# 重启 crond 服务
$ /sbin/service crond restart

# 重新载入配置
$ /sbin/service crond reload

# 加入开机启动
$ chkconfig -level 35 crond on
```

# crontab 文件的含义

用户所建立的 crontab 文件中，每一行都代表一项任务，每行的每个字段代表一项设置，它的格式共分为六个字段，前五段是时间设定段，第六段是要执行的命令段，格式如下：

    minute   hour   day   month   week   command     顺序：分 时 日 月 周

其中：

- minute： 表示分钟，可以是从0到59之间的任何整数。
- hour：表示小时，可以是从0到23之间的任何整数。
- day：表示日期，可以是从1到31之间的任何整数。
- month：表示月份，可以是从1到12之间的任何整数。
- week：表示星期几，可以是从0到7之间的任何整数，这里的0或7代表星期日。
- command：要执行的命令，可以是系统命令，也可以是自己编写的脚本文件。

在以上各个字段中，还可以使用以下特殊字符：

- 星号（*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。
- 逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”
- 中杠（-）：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”
- 正斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如*/10，如果用在minute字段，表示每十分钟执行一次。