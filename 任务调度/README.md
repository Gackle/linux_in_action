# 任务调度

Linux下的任务调度分为两类：**系统任务调度** 和 **用户任务调度**。

## 系统任务调度
系统周期性所要执行的工作，比如写缓存数据到硬盘、日志清理等。在 /etc 目录下有一个 crontab 文件，这个就是系统任务调度的配置文件。

**/etc/crontab** 文件包括下面几行：

``` shell
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=""
HOME=/

# run-parts
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
```
前四行是用来配置 crond 任务运行的环境变量：
1. 第一行 `SHELL` 变量指定了系统要使用哪个 shell，这里是 bash；
2. 第二行 `PATH` 变量指定了系统执行命令的路径
3. 第三行 `MAILTO` 变量指定了crond 的任务执行信息将通过电子邮件发送给 root 用户，如果 `MAILTO` 变量的值为空，则表示不发送任务执行信息给用户
4. 第四行的 `HOME` 变量指定了在执行命令或者脚本时使用的主目录。


## 用户任务调度

用户定期要执行的工作，比如用户数据备份、定时邮件提醒等。用户可以使用 crontab 工具来定制自己的计划任务。所有用户定义的 crontab 文件都被保存在 **/var/spool/cron** 目录中。其文件名与用户名一致，使用者权限文件如下：

- /etc/cron.deny     该文件中所列用户不允许使用 `crontab` 命令
- /etc/cron.allow    该文件中所列用户允许使用 `crontab` 命令
- /var/spool/cron/   所有用户 cron 时间表存放的目录, 以用户名命名

## 任务优先级

在多任务操作系统中，内核负责将 CPU 时间分配给系统上运行的每个进程。

**调度优先级**（scheduling priority）是内核分配给进程的 CPU 时间（相对于其他进程）。在 Linux 系统中，由 shell 启动的所有进程的调度优先级默认都是相同的。 

调度优先级是个整数值，从 -20（最高优先级）到 +19（最低优先级）。默认情况下，bash shell 以优先级 0 来启动所有进程。 

> <small>最低值 -20 是最高优先级，而最高值 +19 是最低优先级，这太容易记混了。只要记住那句俗语“好人难做”就行了。越是“好”或高的值，获得 CPU 时间的机会越低。 </small>