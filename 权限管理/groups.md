---
description: 组权限命令集合
---

# groups 命令

`groups` 命令在 stdout 上输出指定用户所在组的组成员，每个用户属于 `/etc/passwd` 中指定的一个组和在 `/etc/group` 中指定的其他组。

## 命令用法

``` shell
groups [options]... [username]...
```

不给出 `username` 的情况下默认显示全部工作组。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| --help | 显示帮助信息 |
| --version | 输出版本号并退出 |

# groupadd 命令

`groupadd` 命令用于创建一个新的工作组，新工作组的信息将被添加到系统文件中。

## 命令用法 

``` shell
groupadd [options]... groupname
```

`groupadd` 新创建的组 `groupname` 一开始是不会有用户的，我们可以使用 `usermod` 添加用户。

## 常用可选参数

| 参数 | 选项 |
|:---|:---|
| -f, --force | 如果组已存在则成功退出 |
| -g, -gid GID | 为新工作组指定 `GID` |
| -k, --key KEY=VALUE | 复写 `/etc/login.defs` 的默认设置 |
| -r, --system | 建系统工作组，系统工作组的组ID小于500 |
| -o, --non-unique | 允许创建有重复 GID 的工作组 |

# groupdel 命令

`groupdel` 命令用于删除指定的工作组，本命令要修改的系统文件包括 **/ect/group** 和 **/ect/gshadow**。

若该群组中仍包括某些用户，则必须先删除这些用户后，方能删除群组。

## 命令用法

``` shell
groupdel [options]... groupname
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -f, --force | 即使是一个用户的私有工作组也要强制删除 |

# groupmod 命令

`groupmod` 命令更改群组识别码或名称。需要更改群组的识别码或名称时，可用 `groupmod` 指令来完成这项工作。

## 命令用法

``` shell
groupmod [options]... groupname
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -g, --gid GID | 更改工作组的 ID 为 `GID` |
| -n, --new-name NEW_GROUP | 更改工作组的名字为 `NEW_GROUP` 字符串 |
| -o, --non-unique | 允许使用重复的 GID |
