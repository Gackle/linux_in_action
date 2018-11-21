# 为用户添加 sudo 权限

## 1. 使用 visudo（Ubuntu）

`visudo` 以安全模式编辑 `sudoers` 文件。`visudo` 锁定 `sudoers` 文件以防多个编辑同时进行，提供基本的检查（sanity checks）和语法错误检查。如果 `sudoers` 文件现在正在被编辑，你会收到提示稍后再试。

## 2. 直接修改 /etc/sudoers

方法 1 的本质也是修改 */etc/sudoers* 文件。如果我们编辑 `/etc/sudoers` 文件，就会发现它以注释的方式提供了一些常用的例子：

``` shell
# /etc/sudoers 文件配置的格式：哪个用户可以在那台机器上运行哪个命令（sudoer 文件可以跨多个系统共享）
#   user    MACHINE=COMMANDS
# 允许 sys 用户组的成员运行 networking, software, service management apps 等等
%sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING, PROCESSES, LOCATE, DRIVERS
# 运行 wheel 用户组的成员运行所有命令（括号中的 ALL 表示可以切换的身份）
%wheel  ALL=(ALL)    ALL
# 和上面类似，不过使用 sudo 时不需要密码
%wheel  ALL=(ALL)   NOPASSWD: ALL
# 允许 users 用户组的成员以 root 用户的身份挂载和卸载 cdrom
%users  ALL=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom
```

## 3. 加入用户组 wheel（CentOS）

CentOS 默认情况下，wheel 用户组都被授予了 `sudo` 的访问权限，因此我们可以：

``` bash
usermod -aG wheel [username]
```

# sudo 命令

Linux `sudo` 命令以系统管理者的身份执行指令，也就是说，经由 `sudo` 所执行的指令就好像是 root 亲自执行。

## 命令用法

``` bash
$ sudo [-D level] -h | -K | -k | -V
$ sudo -v [-AknS] [-D level] [-g groupname|#gid] [-p prompt]
            [-u user name|#uid]
$ sudo -l[l] [-AknS] [-D level] [-g groupname|#gid] [-p
            prompt] [-U user name] [-u user name|#uid] [-g
            groupname|#gid] [command]
$ sudo [-AbEHknPS] [-r role] [-t type] [-C fd] [-D level] [-g
            groupname|#gid] [-p prompt] [-u user name|#uid] [-g
            groupname|#gid] [VAR=value] [-i|-s] [<command>]
$ sudo -e [-AknS] [-r role] [-t type] [-C fd] [-D level] [-g
            groupname|#gid] [-p prompt] [-u user name|#uid] file ..
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -b | 在后台运行命令 |
| -C fd | 关闭所有大于 `fd` 的文件描述符 |
| -E | 当运行命令时保留当前用户的环境 |
| -g group | 以指定用户组 group 成员的身份运行命令 |
| -H | 将环境变量的 `$HOME` 指定为目标用户的 HOME 目录 |
| -i | 以目标用户的身份打开其交互式 shell ，和 `-s` 的区别是，它给到的将会是 root 环境 |
| -k | 强制使用者在下一次执行 `sudo` 是必须询问密码 |
| -l[l] command | 列出用户的可以 `sudo` 执行的命令 |
| -s | 以目标用户身份执行一个交互式 shell ，shell 具有 root 权限但不是 root 环境（依旧使用自己的 .bashrc）|
| -S | 从标准输入读取密码 |
| -- | 停止处理命令行参数 |
