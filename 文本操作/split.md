---
description: split 命令 —— 将一个大文件分割成很多个小文件
---

# split 命令

`split` 命令可以将一个大文件分割成很多个小文件，有时需要将文件分割成更小的片段，比如为提高可读性，生成日志等。

## 命令用法

``` bash
$ split [OPTION]... [FILE [PREFIX]]
```

将文件 `FILE` 分割为 `PREFIXaa`、`PREFIXab` 等多个文件，其中：

- 默认每 1000 行划分为一个文件，而且默认的前缀 `PREFIX` 为 `x`;
- 如果没有指定 `FILE` 或者 `FILE` 为 `-`，则从标准输入读取。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -a, --suffix-length=N | 以长度 N 作为划分后的输出文件后缀，默认 N 为 2，即 `aa`, `ab`, `ac` |
| --additional-suffix=SUFFIX | 给文件名添加一个 `SUFFIX` 的后缀 |
| -b, --bytes=SIZE | 以指定的 `SIZE` 字节大小来划分文件 |
| -C, --line-bytes=SIZE | 设置每一个输出文件最多有 `SIZE` 个字节大小 |
| -d | 使用以 0 开始的数字作为后缀而不使用字母后缀 |
| --numeric-suffixes[=FROM] | 和 `-d` 相同，不过允许你设置起始数字 |
| -e, --elide-empty-files | 配合 `-n` 使用，不生成空的输出文件 |
| -l, --lines=NUMBER | 以指定的行数或记录数 `NUMBER` 来划分文件 |
| -n, --number=CHUNKS | 以指定的块 `CHUNKS` 来划分并输出文件 |
| -t, --separator=SEP | 使用指定的 `SEP` 字符而不是新的一行作为行划分的分隔符 |
| --verbose | 显示运行状态信息 |

以上的 `SIZE` 参数是一个整数加上一个可选的单位（例如 `10K` 是 `10*1024`）；  
单位可以是 K,M,G,T,P,E,Z,Y （以 1024 为阶）或者 KB,MB...（以 1000 为阶）

## CHUNK 参数 

| 参数 | 说明 |
|:--- |:---|
| N | 根据输入文件的大小平均划分为 N 个文件 |
| K/N | 划分为 N 个文件，输出其中的第 K 个文件到 stdout 标准输出中 |
| l/N | 划分为 N 个文件，但不划分行或者记录 |
| l/K/N | 划分为 N 个文件，但不划分行或者记录，输出其中的第 K 个文件到 stdout 标准输出中 |
| r/N | 和 `l` 类似但使用 round robin distribution 算法来划分 |
| r/K/N | 和上面的参数类似但只输出第 K 个文件到标准输出 |

## 使用实例

``` bash
# 以 3 行为单位划分文件，指定 Split 为文件前缀，同时以数字作为划分标记后缀
$ split --help | split -d --verbose -l 3 - Split
creating file 'Split00'
creating file 'Split01'
creating file 'Split02'
creating file 'Split03'
creating file 'Split04'
creating file 'Split05'
creating file 'Split06'
creating file 'Split07'
creating file 'Split08'
creating file 'Split09'
creating file 'Split10'
creating file 'Split11'
creating file 'Split12'
$ ls
Split00  Split01  Split02  Split03  Split04  Split05  Split06  Split07  Split08  Split09  Split10  Split11  Split12
```