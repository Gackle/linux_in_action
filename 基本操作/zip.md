---
description: 解压缩命令集合
---

# compress 命令

`compress` 命令使用 *Lempress-Ziv* 编码压缩数据文件。compress 是个历史悠久的压缩程序，文件经它压缩后，其名称后面会多出 **`.Z`** 的扩展名。

当要解压缩时，可执行 `uncompress` 指令。但实际上 `uncompress` 只是 `compress` 的符号链接，因此解压缩和压缩文件都可以用 `compress` 完成。

## 命令用法

``` bash
$ compress [OPTION]... [FILE]...
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -c | 输出结果至标准输出设备 stdout |
| -d | 解压缩文件 |
| -r | 进行递归操作 |
| -b RANGE | 压缩率，介于 9~16 的数值，预设值为"16"，指定愈大的数值，压缩效率就愈高 |
| -f | 强制写入文档，若文档已存在，则会被覆盖 |
| -v | 显示命令执行过程 |


# zip 命令

`zip` 命令可以用来解压缩文件，或者对文件进行打包操作。zip是个使用广泛的压缩程序，文件经它压缩后会另外产生具有 **`.zip`** 扩展名的压缩文件。



# gzip 命令

`gzip` 命令用于解压文件以及压缩文件（默认是原地压缩）。文件经过其压缩过后，其名称会多出 **`.gz`** 扩展名。

## 命令用法

``` bash
$ gzip [OPTION]... [FILE]...
```

如果 `FILE` 没有输入或者 `FILE` 的值是 `-`，从标准输入读取。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -c, --stdout | 把压缩后的文件输出到标准输出设备 stdout ，不去更动原始文件 |
| -d, --decompress | 解压缩文件 |
| -f, --force | 强制压缩文件，无论文件名或硬链接是否存在 |
| -k, --keep | 不删除输入文件 | 
| -l, --list | 列出压缩文件的相关信息 |
| -n, --no-name | 压缩文件时，不保存或存储原始的文件名和时间戳 |
| -N, --name | 压缩文件时，保存或存储原始的文件名和时间戳 |
| -q, --quiet | 不显示警告信息 |
| -r, --recursive | 递归处理，将指定目录下的所有文件和子目录一并处理 |
| -v, --verbose | 显示执行过程 |
| -1, --fast | 最快压缩效率 |
| -9, --best | 最优压缩质量 |
| -t, --test | 测试压缩文件是否无误 |

## 使用实例

1. 压缩当前目录
    ``` bash
    # 列出当前目录文件
    gackle@machine:/Project$ ls
    backend.md  main.cpp  main.exe  main_linux.exe  main.obj
    # 压缩当前目录
    gackle@machine:/Project$ gzip *
    gackle@machine:/Project$ ls
    
    backend.md.gz  main.cpp.gz  main.exe.gz  main_linux.exe.gz  main.obj.gz
    # 不修改源文件
    gackle@machine:/Project$ gzip -kv *
    backend.md:      58.6% -- replaced with backend.md.gz
    main.cpp:        45.4% -- replaced with main.cpp.gz
    main.exe:        47.0% -- replaced with main.exe.gz
    main_linux.exe:  66.8% -- replaced with main_linux.exe.gz
    main.obj:        76.3% -- replaced with main.obj.gz

    gackle@machine:/Project$ ls
    backend.md     main.cpp     main.exe     main_linux.exe     main.obj
    backend.md.gz  main.cpp.gz  main.exe.gz  main_linux.exe.gz  main.obj.gz
    ```

2. 解压文件
    ``` bash
    gackle@machine:/Project$ gzip -dv *
        backend.md.gz:   58.6% -- replaced with backend.md
        main.cpp.gz:     45.4% -- replaced with main.cpp
        main.exe.gz:     47.0% -- replaced with main.exe
        main_linux.exe.gz:       66.8% -- replaced with main_linux.exe
        main.obj.gz:     76.3% -- replaced with main.obj
    ```

3. 显示压缩文件信息
    ``` bash
    gackle@machine:/Project$ gzip -l *
            compressed        uncompressed  ratio uncompressed_name
                1948                4630    58.6%     backend.md
                444                 764     45.4%     main.cpp
                118954              224256  47.0%     main.exe
                3059                9112    66.8%     main_linux.exe
                35433              149686   76.3%     main.obj
                159838             388448   58.9%     (totals)
    ```

# bzip2 命令

`bzip2` 命令用于创建和管理（包括解压缩） **`.bz2`** 格式的压缩包。

## 命令用法

``` bash
$ bzip2 [flags and input files in any order]
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -d, --decompress | 解压缩文件 |
| -z, --compress | 压缩文件 |
| -t, --test | 测试压缩文件的完整性 |
| -k, --keep | 保持输入文件不变更（被删除）|
| -f, --force | 覆写已存在的输出文件 |
| -v, --verbose | 显示命令执行过程 |
| -c, --stdout | 输出到标准输出 stdout |
| -1 ... -9 | 设置压缩块大小为 100K ~ 900K |
| -s, --small | 使用最小内存（最大占用为 2500K） |
| --fast | 等同于 `-1` |
| --best | 等同于 `-9` |

## 使用实例

1. 压缩当前目录的文件（不删除源文件）
    ``` bash
    gackle@machine:/Project$ bzip2 -k *

    gackle@machine:/Project$ ls
    
    backend.md  backend.md.bz2  main.cpp  main.cpp.bz2  main.exe  main.exe.bz2  main_linux.exe  main_linux.exe.bz2  main.obj  main.obj.bz2
    ```
2. 显示压缩文件内容
    ``` bash
    gackle@machine:/Project$ bzip2 -dc *.bz2
    # 等同于
    gackle@machine:/Project$ bzcat *bz2
    ```