---
description: free 命令 —— 查看系统上可用的和已用的内存
---

# free 命令

`free` 命令可以显示当前系统未使用的和已使用的内存数目，还可以显示被内核使用的内存缓冲区。在 Linux 系统监控的工具中，free命令是最经常使用的命令之一。

## 命令用法

``` bash
$ free [options]
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -b, --bytes | 以 bytes 为单位输出 |
| --kilo | 以 KB 为单位输出 |
| --mega | 以 MB 为单位输出 |
| --giga | 以 GB 为单位输出 |
| --tera | 以 TB 为单位输出 |
| --peta | 以 PB 为单位输出 |
| -k, --kibi | 以 KiB 为单位输出 |
| -m, --mebi | 以 MiB 为单位输出 |
| -g, --gibi | 以 GiB 为单位输出 |
| -h, --human | 以可读性较好的形式输出 |
| -t, --total | 显示 RAM 和 swap 的内存总和信息 |
| -s N, --seconds N | 每 `N` 秒重复打印 |
| -c N, --count N | 重复打印 `N` 次，然后退出 |
| --si | 使用 1000 为进位而不是 1024 |

## 结果参数解析

``` bash
gackle@machine:~$ free -h
            total        used        free      shared  buff/cache   available
Mem:           7.9G        6.6G        1.0G         17M        223M        1.1G
Swap:           24G        727M         23G
```

其中：
- `total` 内存总数
- `used` 已经使用的内存数
- `free` 空闲的内存数
- `shared` （此列已废弃不用）
- `buff` 缓冲内存数
- `cache` 缓存内存数


## 使用实例
1. 显示目前内存信息
    ``` bash
    gackle@machine:~$ free -h
                total        used        free      shared  buff/cache   available
    Mem:           7.9G        6.6G        1.0G         17M        223M        1.1G
    Swap:           24G        727M         23G
    ```
2. 显示总和信息
    ``` bash
    gackle@machine:~$ free -th
              total        used        free      shared  buff/cache   available
    Mem:           7.9G        6.7G        1.0G         17M        223M        1.1G
    Swap:           24G        726M         23G
    Total:          31G        7.4G         24G
    ```
