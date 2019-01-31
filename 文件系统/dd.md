---
description: dd 命令 —— 用于读取、转换并输出数据
---

# dd 命令

`dd` 可从标准输入或文件中读取数据，根据指定的格式来转换数据，再输出到文件、设备或标准输出。一般用于制作 Linux 系统盘，用 `dd` 命令进行两块硬盘的复制，它除了能够复制文件中的数据，还能够复制分区和文件系统，可以完整地复制出一块和原系统盘一样的硬盘。

## 命令用法

``` shell
dd [OPERAND] ...
dd OPTION
```

## 常用可选参数

### OPERAND 格式化参数

| 参数 | 说明 |
|:---|:---|
| bs=BYTES | 一次读/写 BYTES 个字节 |
| cbs=BYTES | 一次转换 BYTES 个字节 |
| conv=CONVS | 根据 symbol list（符号表，以逗号分隔）的格式转换文件 |
| count=BLOCKS | 仅从输入块中拷贝 BLOCKS 个块 |
| ibs=BYTES | 一次读取 BYTES 个字节（默认 512） |
| if=FILE | 从文件而不是标准输入中读取 |
| iflag=FLAGS | 根据 symbol list（符号表，以逗号分隔）指定的格式读取 |
| obs=BYTES | 一次写入 BYTES 个字节（默认 512） |
| of=FILE | 写入到文件而不是标准输出 |
| oflag=FLAGS | 根据 symbol list（符号表，以逗号分隔）指定的格式写入 |
| seek=BLOCKS | 在输出的开头跳过 BLOCKS 个 obs-sized 大小的块 |
| skip=BLOCKS | 在输入的开头跳过 BLOCKS 个 ibs-size 大小的块 |
| status=WHICH | WHICH 的信息用来控制输出到标准错误的内容，`noxfer` 不显示转换的统计， `none` 则全都不显示 |

### CONV 格式化参数

| 参数 | 说明 |
|:---|:---|
| ascii | 将 EBCDIC 编码转为 ASCII 编码 |
| ebcdic | 将 ASCII 编码转为 EBCDIC 编码 |
| ibm | 将 ASCII 编码转为 alternate EBCDIC 编码 |
| block | 将每一行（带有换行符）的长度填充为 cbs-size 的大小 |
| unblock | 将每一个 cbs-size 大小的记录的尾随空格以换行符替换 |
| lcase | 将大写字母换为小写字母 |
| nocreat | 不要创建新的输出文件 |
| excl | 如果输出文件已存在则失败 |
| notrunc | 不要删除输出文件 |
| ucase | 将小写字母换为大写字母 |
| sparse | 对于为 NUL 的输入文件，尝试寻找而不是写入输出 |
| swab | 交换每对输入字节 |
| noerror | 当读取出错后继续执行 |
| sync | 用 NUL 填充每个输入块直至大小为 ibs-size ；当与 block 或 unblock 一起使用时，则使用空格而不是 NUL |
| fdatasync | 在结束前就写入到物理的输出文件上 |
| fsync | 和上面一样，但是也会写入元数据 |

### FLAG 格式化参数

| 参数 | 说明 |
|:---|:---|
| append | 使用追加模式 |
| direct | 对数据使用 direct I/O |
| directory | 除非是目录，否则操作失败 |
| dsync | 对数据使用 synchronized I/O |
| sync | 和上面一样，但也会作用于元数据 |
| fullblock | （仅针对 iflag）累加完整的输入块 |
| nonblock | 使用 non-blocking I/O |
| noatime | 不要更新其访问时间 |
| noctty | 不要从文件中分配控制终端（controlling terminal） |
| nofollow | 不处理符号链接 |

### 可选参数

| 参数 | 说明 |
|:---|:---|
| --help | 显示帮助信息并退出 |
| --version | 输出版本信息并退出 |

## 使用实例

1. 发送一个 USR1 信号到一个 `dd` 处理进程会让他打印出 I/O 信息到标准错误，然后恢复拷贝

    ``` bash
    $ dd if=/dev/zero of=/dev/null& pid=$!
    $ kill -USR1 $pid; sleep 1; kill $pid
    18335302+0 records in
    18335302+0 records out
    9387674624 bytes (9.4 GB) copied, 34.6279 seconds, 271 MB/s
    ```

2. 备份与恢复

    ``` bash
    # 将 /dev/hdb 全盘数据被分到 image 文件
    $ dd if=/dev/hdb of=/root/image
    # 将备份文件恢复到指定盘
    $ dd if=/root/image of=/dev/hdb
    ```

3. 拷贝内存内容到硬盘

    ``` bash
    # 指定块大小为 1024
    $ dd if=/dev/mem of=/root/mem.bin bs=1024
    ```
