---
description: renice 命令 —— 修改系统上运行中应用的优先级
---

# renice 命令

`renice` 命令可以修改正在运行的进程的调度优先级。它允许你指定运行进程的 PID f来改变它的优先级。 

`renice` 命令会自动更新当前运行进程的调度优先级。和 `nice` 命令一样，`renice` 命令也有一 些限制：
- 只能对属于你的进程执行 `renice`;
- 只能通过 `renice` 降低进程的优先级； - root 用户可以通过 `renice` 来任意调整进程的优先级。 

如果想完全控制运行进程，必须以 root 账户身份登录或使用 sudo 命令。 

## 命令用法

``` shell
$ renice [-n] <priority> [-p|--pid] <pid>...
$ renice [-n] <priority>  -g|--pgrp <pgid>...
$ renice [-n] <priority>  -u|--user <user>...
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -n, --priority <num> | 指定要调整的优先级（谦让度级别）|
| -p, --pid <id> | 以程序进程号 PID 作为入参（默认） |
| -g, --pgrp <id> | 以进程组号 GID 作为入参，调整进程组优先级 |
| -u, --user <name>|<id> | 以用户名或用户 ID uid 作为入参，调整改用户的进程优先级 |

## 使用实例

1. 将进程id为 987 以及 32 的进程和进程拥有者为 daemon 和 root 的优先级调低

``` bash
$ renice 1 987 -u daemon root -p 32
```