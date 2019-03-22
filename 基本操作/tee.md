# tee 命令

`tee` 命令用于从标准输入 stdin 中读取数据，将其内容输出到标准输出设备 stdout，同时保存为文件。

## 命令用法

``` bash
tee [OPTION]... [FILE]...
```

`tee` 负责将标准输入 copy 到每一个 FILE 上，同时输出到标准输出 stdout 上。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -a, --append | 追加内容到给定的 FILE 上而不是覆盖它们 |
| -i, --ignore-interrupts | 忽略中断信号 |

## 使用实例

`tee` 命令一般来说是用来满足那些光靠管道重定向符 `<` 无法解决的同时输出内容的问题。

``` bash
# ls 打印当前目录内容，同时写入到 output.txt 中
$ ls | tee output.txt | cat -n
     1  bin
     2  myapp.csproj
     3  obj
     4  output.txt
     5  Program.cs
```