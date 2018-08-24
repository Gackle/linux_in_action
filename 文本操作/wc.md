---
description: wc 命令 —— 计算文件字数信息
---

# wc 命令

wc 命令用于打印指定每个文件的行数、单词数以及字节数，如果给定多个文件，还会显示总行数。一个单词的定义是以空格分隔得到的非零字符序列。

如果没有指定文件或者指定 `-`，则从标准输入读取。

## 命令用法

``` shell
$ wc [OPTION]... [FILE]...
$ wc [OPTION]... --files0-from=F
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -c, --bytes | 打印字节数 |
| -m, --chars | 打印字符数 |
| -l, --lines | 打印行数 |
| -L, --max-line-length | 打印一行最长显示的宽度 |
| -w, --words | 打印单词数 |
| --files0-from=F | 从文件 `F` 中读取非空终止名称作为指定的输入，如果 `F` 为 `-`，则从标准输入读取 | 

> <small> 非空终止字符：不以 `\0` 结尾的字符 </small>

## 结果参数解析

``` shell
$ wc *.py
   44    93  1191 cookie_counter.py
   69   119  2072 cookies.py
   37    77  1116 definitions_readonly.py
   50   107  1569 definitions_readwrite.py
   27    67   855 hello_errors.py
   33    60   893 hello_module.py
   35   116  1948 hello.py
   37    74  1146 poemmaker.py
   38    72  1275 string_service.py
   51   133  2066 tweet_rate_async.py
   50   127  1920 tweet_rate_gen.py
   43   120  1672 tweet_rate.py
  514  1165 17723 total
```

从左到右分别是行数、单词数、字符数、字节数以及最大行宽。默认显示 **行数**、**单词数**、**字节数** 和 文件名。


## 使用实例

1. 统计当前目录以及子目录下所有文件的行数 

``` shell
$ wc -l `find . -type f`
```
