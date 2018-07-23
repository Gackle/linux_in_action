---
description: xxd 命令
---

# xxd 命令

`xxd` 命令对于标准输入或者给定的文件，显示其16进制的内容。也可以反过来进行转换。

## 命令用法

``` shell
$ xxd [options] [infile [outfile]]
```

其中，
- infile 表示要输入进行 16 进制编码的文件
- outfile 表示转换结果的输出文件

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -b | 用二进制现实一个 bit，而不是使用十六进制 |
| -r | 以十六进制作为输入，二进制作为输出 |
| -l NUM | 只输出 `NUM` 个字符 |
| -u | 十六进制输出时使用大写字母，默认时小写字母 |
| -i | 以 C 语言 include 文件的形式输出 |
| -h | 输出概要信息 |
| -r -s offset | 调整当前位置的偏移位置 `offset` |
| -s [+][-]seek | 调整开始位置的偏移位置 `seek`，+ 为绝对偏移，- 为相对偏移 |

## 使用实例
1. 显示十六进制格式
    ``` bash
    gackle@machine:~$ echo 1111111 > 1.txt

    gackle@machine:~$ cat 1.txt
    1111111

    gackle@machine:~$ xxd 1.txt
    00000000: 3131 3131 3131 310a                      1111111.
    ```
2. 转换为二进制形式显示
    ``` bash
    gackle@machine:~$ xxd 1.txt |xxd -r
    1111111
    ```