---
description: nohup 命令 —— 运行命令，忽略挂断（hangup）信号
---

# nohup 命令

一般情况下，我们会在命令 *COMMAND* 后面加上 `&` 来让命令后台执行，但问题是，如果我们把当前的终端关闭了，命令也会一并终止执行。那么 `nohup` 就是来完成这个“不停机”运行命令的功能，一般情况下我们都会配合 `&` 一起使用，以达到在后台持续运行的目的。

## 命令用法

``` bash
nohup COMMAND [ARG]...
nohup OPTION
```

## 注意事项

+ 如果标准输入是一个终端，那么会将它重定向到 */dev/null*
+ 如果标准输出是一个终端，会以 **追加** 的形式将输出结果写到 `nohup.out` 中；如果没有这个文件，则写到 `$HOME/nohup.out` 中
+ 如果标准错误是一个终端，那么会将它重定向到标准输出
+ 像将输出结果保存到文件，请使用 `nohup COMMAND > FILE`

## 命令常用用法

从 input.file 中读取参数，执行 COMMAND （`python application.py`）并将输出结果重定向到 myout.file ，在后台静默运行

``` bash
nohup python application.py > myout.file <input.file 2>&1 &
```

## nohup 和 & 区别

`nohup`: 指不挂断的运行，注意并没有后台运行的意思。
`&`： 指后台运行，当用户退出（挂起）时，命令也会跟着退出。
