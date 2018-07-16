---
description: ls 命令 —— 显示目标列表
---
# ls 命令 

`ls` 命令用于显示目标的列表，是 Linux 中使用频率较高的命令。

## 命令用法

``` shell
$ le [OPTIONs] [FILEs]
```

其中 `FILEs` 默认为当前目录。

## 常用可选参数 ##

| 参数 | 说明 |
|:---|:---|
| -a | 显示所有的文件以及目录（包括 `.` 和 `..` ） |
| -A | 显示所有的文件以及目录（不包括 `.` 和 `..`）。这是默认选项 |
| --time=atime | 显示文件或目录的访问时间 |
| -d | 仅显示目录名，而不显示目录下的内容列表。显示符号链接文件本身，而不显示其所指向的目录列表 |
| -C | 多列显示输出结果。这是默认选项 |
| -l | 和 -C 相反，以单列的形式输出 |
| -t | 根据目录和文件的 **更改时间** 排序 |
| -c | 等同于 `-lt` |
| -R | 递归显示指定目录下的所有文件以及子目录 |
| -s | 显示文件和目录的大小，以区块为单位 |
| -k | 显示文件和目录的大小，以 KB(千字节) 为单位 |
| -i | 显示文件的索引号 inode |
| -F | 在每个输出项后追加文件的类型标识符，具体含义：`*` 表示具有可执行权限的普通文件，`/` 表示目录，`@` 表示符号链接，`|` 表示命令管道FIFO，`=` 表示sockets套接字。当文件为普通文件时，不输出任何标识符 |
| --file-type | 与 -F 选项的功能相同，但是不显示 `*` |
| -h | 通常和 -l/-s 何用，以人类可读的格式输出文件以及目录大小 |


## 结果分析 ##

``` shell
gackle@machine:/Projects/tornadoproject$ ls -lsaFh
total 48K
   0 drwxrwxrwx 1 gackle gackle  512 Jul  9 14:56  ./
   0 drwxrwxrwx 1 gackle gackle  512 Jul 16 16:23  ../
   0 drwxrwxrwx 1 gackle gackle  512 Jul  6 14:01 "Burt's Book"/
4.0K -rwxrwxrwx 1 gackle gackle 1.2K Jul  9 11:31  cookie_counter.py*
4.0K -rwxrwxrwx 1 gackle gackle 2.1K Jul  9 14:24  cookies.py*
4.0K -rwxrwxrwx 1 gackle gackle 1.1K Jul  6 11:15  definitions_readonly.py*
4.0K -rwxrwxrwx 1 gackle gackle 1.6K Jul  6 11:29  definitions_readwrite.py*
4.0K -rwxrwxrwx 1 gackle gackle  855 Jul  5 19:26  hello_errors.py*
4.0K -rwxrwxrwx 1 gackle gackle  893 Jul  6 09:12  hello_module.py*
4.0K -rwxrwxrwx 1 gackle gackle 2.0K Jun 29 12:00  hello.py*
   0 drwxrwxrwx 1 gackle gackle  512 Jul  9 11:40  notes/
4.0K -rwxrwxrwx 1 gackle gackle 1.2K Jul  5 14:06  poemmaker.py*
   0 drwxrwxrwx 1 gackle gackle  512 Jul  9 10:30 'Shopping Cart'/
4.0K -rwxrwxrwx 1 gackle gackle 1.3K Jul  4 14:48  string_service.py*
   0 drwxrwxrwx 1 gackle gackle  512 Jul  9 14:17  templates/
   0 drwxrwxrwx 1 gackle gackle  512 Jul  5 15:44 'The Alpha Munger'/
4.0K -rwxrwxrwx 1 gackle gackle 2.1K Jul  6 17:49  tweet_rate_async.py*
4.0K -rwxrwxrwx 1 gackle gackle 1.9K Jul  9 04:32  tweet_rate_gen.py*
4.0K -rwxrwxrwx 1 gackle gackle 1.7K Jul  6 17:12  tweet_rate.py*
```

输出的第一行显示了在目录中包含的总块数，在此之后每一行都包含了关于文件（或目录）的下述信息。

- 文件类型，比如目录（d）、文件（-）、字符型文件（c）或块设备（b）；
- [文件的权限](README.md#authorization)
- 文件的硬链接总数
- 文件属主的用户名
- 文件属组的组名
- 文件的大小（以字节为单位）
- 文件的上次修改该时间
- 文件名或目录名