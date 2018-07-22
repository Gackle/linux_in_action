---
description: 用户权限命令集合
---

# useradd 命令

`useradd` 命令用于Linux中创建的新的系统用户。帐号建好之后，再用 `passwd` 设定帐号的密码。使用 `useradd` 指令所建立的帐号，实际上是保存在 **/etc/passwd** 文本文件中。

## 命令用法

``` shell
$ useradd [options] [login]
```

在使用 `-D` 参数的情况下可以不提供 `login` 用户名参数

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -c, --comment COMMENT | 加上备注文字 `COMMENT`。备注文字会保存在 passwd 的备注栏位中 |
| -d, --home-dir HOME_DIR | 指定新用户登入时的启动目录为 `HOME_DIR` |
| -D, --defaults | 显示或设置 `useradd` 命令的默认配置 |
| -e, --expiredate EXPIRE_DATE | 指定新用户的有效日期为 `EXPIRE_DATE` |
| -f, --inactive INACTIVE | 指定在密码过期后多少天即关闭该用户账户 |
| -g, --gid GROUP | 指定新用户的所属工作组的名字或 ID |
| -G, --groups GROUPS | 指定新用户的附加工作组列表 `GROUPS` |
| -m, --create-home | 自动建立用户的登入目录 |
| -M, --no-create-home | 不要自动建立用户的登入目录 |
| -N, --no-user-group | 不要创建和用户同名的工作组 |
| -p, --password PASSWORD | 设置用户密码为 `PASSWORD` |
| -r, --system | 创建系统用户 |
| -u, --uid UID | 指定用户 ID |
| -U, --user-group | 创建和用户同名的工作组 |

## 使用实例

1. 新增用户 Tim，主要组为 sales，次要组为 company employee
    ``` shell
    $ useradd –g sales Tim –G company,employees
    ```

# usermod 命令

`usermod` 能用来修改 **/etc/passwd** 文件中的大部分字段，只需用与想修改的字段对应的命令行参数就可以了。参数大部分跟 `useradd` 命令的参数一样。

## 命令用法

``` shell
$ usermod [options] LOGIN
```

## 常用可见参数

| 参数 | 说明 |
|:---|:---|
| -c, --comment COMMENT | 修改用户帐号的备注文字 |
| -d, --home-dir HOME_DIR | 修改用户登入时的目录为 `HOME_DIR` |
| -e, --expiredate EXPIRE_DATE | 修改帐号的有效期限为 `EXPIRE_DATE` |
| -f, --inactive INACTIVE | 修改在密码过期后多少天即关闭该用户账户 |
| -g, --gid GROUP | 修改用户所属工作组的名字或 ID |
| -G, --groups GROUPS | 改用户所属的附加工作组列表 `GROUPS` |
| -l, --login NEW_LOGIN | 修改用户账户的登录名 |
| -L, --lock | 锁定账户，使用户无法登陆 |
| -m, --move-home | 配合 `-d` 使用，移动旧用户目录的内容到新的用户目录上 |
| -o, --non-unique | 允许使用重复的 uid |
| -p, --password PASSWORD | 修改用户密码 |
| -u, --uid UID | 修改用户的 uid 为 `UID`  |
| -U, --unlock | 解除锁定，使用户能够登录 |

# userdel 命令

如果你想从系统中删除用户，`userdel` 可以满足这个需求。<u>默认情况下，`userdel` 命令会只删除 **/etc/passwd** 文件中的用户信息，而不会删除系统中属于该账户的任何文件</u>。

如果加上 `-r` 参数，`userdel` 会删除用户的 HOME 目录以及邮件目录。然而，系统上仍可能存有已删除用户的其他文件。这在有些环境中会造成问题。 

## 命令用法

``` shell
$ userdel [options] LOGIN
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -f, --force | 强制删除用户，即使用户当前已登录 |
| -r, --remove | 删除用户的同时，删除与用户相关的所有文件 |

> <small>请不要轻易用 `-r` 选项；他会删除用户的同时删除用户所有的文件和目录，切记如果用户目录下有重要的文件，在删除前请备份。</small>

# chfn 命令

`chfn` 命令提供了在 **/etc/passwd** 文件的备注字段中存储信息的标准方法。`chfn` 命令会将用于 Unix 的 `finger` 命令的信息存进备注字段，而不是简单地存入一些随机文本（比如名字或昵称之 类的），或是将备注字段留空。`finger` 命令可以非常方便地查看 Linux 系统上的用户信息。 

> 出于安全性考虑，很多 Linux 系统管理员会在系统上禁用 `finger` 命令，不少 Linux 发行版甚至都没有默认安装该命令。 

## 命令用法

``` shell
$ chfn [options] [login]
```

不给出 `login` 用户名的话默认是修改当前用户。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -f, --full-name FULL_NAME | 更改用户的全名为 `FULL_NAME` |
| -h, --home-phone HOME_PHONE | 更改用户的家庭电话为 `HOME_PHONE` |
| -o, --other OTHER_INFO | 更改用户其他的 CECOS 信息 |
| -r, --room ROOM_NUMBER | 更改用户的房间号为 `ROOM_NUMBER` |
| -w, --work-phone | 更改用户的办公电话为 `WORK_PHONE` |

## 使用实例

``` shell
gackle@machine:~$ chfn gackle
Password:
Changing the user information for kingdee
Enter the new value, or press ENTER for the default
        Full Name:
        Room Number []:
        Work Phone []:
        Home Phone []:
```

# chsh 命令

`chsh` 命令用来更换登录系统时使用的 shell。

## 命令用法

```shell
$ chsh [options] [login]
```

若不指定任何参数与用户名称 `login`，则 `chsh` 会以应答的方式进行设置。

## 常用可选参数
| 参数 | 说明 |
|:---|:---|
| -s, --shell SHELL | 更改系统预设的 shell 环境为 `SHELL`，其中 `SHELL` 为 shell 环境的全路径而不能为 shell 名 |
| -l, --list-shells | 列出目前系统可用的 shell 列表 |