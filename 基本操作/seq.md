---
description: seq 命令 —— 用于产生从某个数到另外一个数之间的所有整数
---

# seq 命令

`seq` 命令类似于 Python 中的 `range` 方法，用于根据指定步长生成连续的整数序列。

## 命令用法

``` bash
$ seq [OPTION]... LAST
# 或者
$ seq [OPTION]... FIRST LAST
# 或者
$ seq [OPTION]... FIRST INCREMENT LAST
```

根据步长 `INCREMENT` 打印从 `FIRST` 到 `LAST` 的整数，其中：

+ 如果 `FIRST` 或 `INCREMENT` 缺省，它默认为 1。也就是说，即使 `LAST` 小于 `FIRST`，`INCREMENT` 也默认为 1
+ 当目前的数字 current 和步长 `INCREMENT` 的和大于 `LAST` 时，序列结束
+ `FIRST`、`INCREMENT` 以及 `LAST` 都会被当作浮点数处理
+ 当 `FIRST` 比 `LAST` 小，`INCREMENT` 通常时正数；当 `FIRST` 比 `LAST` 大，则 `INCREMENT` 通常时负数


## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -f, --format=FORMAT | 使用跟 `printf` 函数打印浮点数的格式一样的参数 `FORMAT` |
| -s, --separator=STRING | 使用 `STRING` 来分隔数字（默认是 `\n`）|
| -w, --equal-width | 通过加入前导 0 来调整输出格式使得输出同宽 |

> `FORMAT` 参数必须是符合打印 double 类型格式的参数，它通常是 `%` 类型的格式


## 使用实例

1. 指定格式
    ``` bash
    $ seq -f "%3g" 1 3 9
        1
        4
        7
    ```
2. 指定输出数字宽度
    ``` bash
    $ seq -w 1 100
    001
    002
    003
    004
    ...
    099
    100
    ```
3. 指定分隔符
    ``` bash
    % seq -s , 2 12
    2,3,4,5,6,7,8,9,10,11,12
    ```