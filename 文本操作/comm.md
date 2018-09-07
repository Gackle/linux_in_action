---
description: comm 命令 —— 两个已排好序文件之间进行逐行比较
---

# comm 命令

`comm` 命令可以用于两个已经排好序的文件之间进行逐行比较，它有一些选项可以用来调整输出，以便执行交集、求差、以及差集操作。

## 命令用法

``` bash
$ comm [OPTION]... FILE1 FILE2
```

其中 `FILE1` 和 `FILE2` 如果其中一个是 `-`（不能两个都是），那么它就会从标准输入读取。

一般情况下，如果没有加入可选选项调节，它的输出内容会包含 3 列：

1. 第一列包含了 `FILE1` 独有的行；
2. 第二列包含了 `FILE2` 独有的行；
3. 第三列包含了它们之间共有的行

## 常用可选参数

| 参数 | 说明 |
|:---:|:---|
| -1 | 不显示在 FILE1 的独有内容（隐藏结果的第一列） |
| -2 | 不显示在 FILE2 的独有内容（隐藏结果的第二列） |
| -3 | 不显示两个的共有内容（隐藏结果的第三列） |
| --check-order | 核对输入文件是否正确的排序 |
| --nocheck-order | 不核对输入文件是否正确的排序 |
| --output-delimiter=STR | 用指定的 `STR` 划分列 |

## 使用实例

## 0. 准备文本

file1.txt 的内容如下：
``` text
line0

line2
line3


line6

line8
line9
line10
```

file2.txt 的内容如下：
``` text
line0
line1


line4
line5


line8

line10
```

稍作排序处理：

``` bash
$ cat file1.txt | sort | uniq | sort > ufile1.txt
$ cat file2.txt | sort | uniq | sort > ufile2.txt
```

### 1. 求两个文本之间的交集

``` bash
$ comm -12 ufile1.txt ufile2.txt

line0
line10
line8
```

### 2. 求两个文本之间的差集

``` bash
# 求 ufile1 - ufile2
$ comm -23 ufile1.txt ufile2.txt
# 求 ufile2 - ufile1
$ comm -13 ufile1.txt ufile2.txt
```

### 3.求两个文本之间的差

``` bash
# 打印出两个文件中不相同的行，并删除第三列
$ comm -3 ufile1.txt ufile2.txt | sed 's/^\t//'
line1
line2
line3
line4
line5
line6
line9
```