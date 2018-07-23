---
description: 磁盘使用情况查看命令集合
---

# df 命令

`df` 命令用于显示磁盘分区上的可使用的磁盘空间。默认显示单位为 KB。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。

## 命令用法

``` bash
$ df [OPTION]... [FILE]...
```

其中 `FILE` 是指定的文件系统上的文件。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -a, --all | 包含全部的文件系统 
| -B, --block-size=SIZE | 以指定的区块大小 `SIZE` 来显示区块数目 |
| -h, --human-readable | 以高可读性的方式来显示信息（以 1024 为换算单位） |
| -H, --si | 和 `-h` 类似，但是在计算时以 1000 为换算单位 |
| -k | 同 `--block-size=1K` |
| -l, --local | 限制仅显示本地的文件系统 |
| -t, --type=TYPE | 限制仅显示某种 `TYPE` 类型的文件系统 |
| -x, --exclude-type=TYPE | 限制仅显示不为 `TYPE` 类型的文件系统 |
| -T, --print-type | 显示文件系统类型 |

## 结果参数解析 

``` bash
gackle@machine:~$ df -ahT
Filesystem     Type         Size  Used Avail Use% Mounted on
rootfs         lxfs         227G  116G  112G  51% /
sysfs          sysfs           0     0     0    - /sys
proc           proc            0     0     0    - /proc
none           tmpfs        227G  116G  112G  51% /dev
devpts         devpts          0     0     0    - /dev/pts
none           tmpfs        227G  116G  112G  51% /run
none           tmpfs        227G  116G  112G  51% /run/lock
none           tmpfs        227G  116G  112G  51% /run/shm
none           tmpfs        227G  116G  112G  51% /run/user
binfmt_misc    binfmt_misc     0     0     0    - /proc/sys/fs/binfmt_misc
C:             drvfs        227G  116G  112G  51% /mnt/c
```

其中：
- FileSystem 代表文件系统
- Type 代表文件系统类型
- Size 表示总占用空间
- Used 表示已用空间
- Avail 表示剩余可使用空间
- Use% 表示使用百分比
- Mounted on 表示挂载点

# du 命令

`du` 命令也是查看使用空间的，但是与 `df` 命令不同的是Linux `du` 命令是对文件和目录磁盘使用的空间的查看。

## 命令用法

``` bash
$ du [OPTION]... [FILE]...
$ du [OPTION]... --files0-from=F
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -a, --all | 显示所有文件的数目而不仅仅只是目录 |
| -B, --block-size=SIZE | 显示目录或文件大小时，以 `SIZE` 为单位 |
| -b, --bytes | 等同于 `--apparent-size --block-size=1` ，以 bytes 为单位显示大小 |
| -c, --total | 除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和 |
| -h, --human-readable | 以高可读性的方式显示统计信息 |
| -L, --dereference | 显示符号链接的源文件 |
| -l, --count-link | 重复计算硬链接的文件 |
| -m | 等同于 `--block-size=1M`，以 MB 为单位输出 |
| -k | 等同于 `--block-size=1K`，以 KB 为单位输出 |
| -P, --no-dereference | 不现实符号链接的源文件（默认选项）|
| -X, --exclude-from=FILE | 排除那些 `FILE` 列表中匹配模式的文件或目录 |
| --exclude=PATTERN | 排除满足模式 `PATTERN` 的文件 |

## 使用实例 

1. 现实指定文件所占空间
    ``` bash
    gackle@machine:~$ du 20.py
    4       20.py
    ```
2. 现实指定目录所占空间
    ``` bash
    gackle@machine:~$ du . -ah
    512     ./bubble_sort.py
    4.0K    ./decorator.py
    4.0K    ./heap_sort.py
    0       ./insert_sort.py
    4.0K    ./merge_sort.py
    4.0K    ./quick_sort.py
    0       ./README.md
    0       ./select_sort.py
    0       ./simple_heap_sort.py
    206K    .
    ```
3. 只显示总和信息
    ``` bash
    gackle@machine:~$ du . -sh
    206k    .
    ```