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

`zip` 命令可以用来压缩文件，或者对文件进行打包操作。zip 是个使用广泛的压缩程序，文件经它压缩后会另外产生具有 **`.zip`** 扩展名的压缩文件。

## 命令用法

``` bash
$ zip [-options] [-b path] [-t mmddyyyy] [-n suffixes] [zipfile list] [-xi list]
```

`zip` 默认的行为是把 `list` 中的文件采用添加或替换的方法压缩到指定的 `zipfile` 当中，如果 `list` 指定的是特殊字符 `-`，则会从标准输入读取并压缩。

如果 `zipfile` 和 `list` 都省略了，则 `zip` 会把标准输入 stdin 的内容压缩到标准输出 stdout 中去。

## 常用可选参数

| 参数 | 说明 | 参数 | 说明 |
|:---|:---|:---|:---|
| -f | 只针对改动文件 | -u | 只针对改动文件和新文件 |
| -d | 从 zipfile 中删除指定内容 | -m | 将 list 文件压缩并加入到 zipfile 中，删除原始文件 |
| -r | 递归处理目录文件 | -j | 丢弃目录信息，只保存文件名称及其内容（有同名文件会导致失败） |
| -0 | 只归档文件，不压缩 | -l | 压缩文件时，将 LF 换成 CR LF （使用 `-ll` 则反过来）|
| -1 | 最快压缩 | -9 | 最优压缩 |
| -q | 静默操作 | -v | 显示过程信息 |
| -c | 为每个压缩到 zipfile 的文件都添加注释| -z | 添加压缩文件 zipfile 的注释 |
| -@ | 从标准输入中读取要 zip 的文件名 | -o | 将 zipfile 的更改时间同步为它其中更新时间最新的文件的更新时间 |
| -x | 排除 list 中列出文件 | -i | 只处理 list 中列出的文件 |
| -F | 尝试修复已损坏的 zipfile | -D | zipfile 内不建立目录 |
| -A | 自动解压缩文件 | -e | 加密 |
| -T | 测试压缩文件的完整性 | -h2 | 显示更多帮助信息 |

## 使用实例

1. 压缩指定目录（静默操作）
    ``` bash
    gackle@machine:/Project$ zip -r1q test dotnetcore/
    gackle@machine:/Project$
    test.zip    dotnetcore
    ```


# unzip 命令

`unzip` 命令用于解压缩由 `zip` 命令压缩的 `.zip` 压缩包。

> `unzip` 在这里的其他命令之中显得非常特殊，因为 `zip` 是没有办法使用自己来解压其压缩的文件，因此需要额外的命令

## 命令用法

``` bash
$ unzip [-Z] [-opts[modifiers]] file[.zip] [list] [-x xlist] [-d exdir]
```

其中:
- `unzip -Z` 相当于执行 `zipinfo` 命令，打印压缩文件信息
- 默认是在当前目录解压缩那些在 `list` 列表的文件，排除在 `xlist` 列表中的文件；若指定了 `exdir` 则解压到对应的 `exdir` 目录中


## 常用可选参数 

| 参数 | 说明 | 参数 | 说明 |
|:---|:---|:---|:---|
| -p | 解压 zipfile 内容到管道 pipe 上 | -l | 以短格式列出 zipfile 中包含的文件 |
| -f | 更新现有的文件而不重新创建 | -t | 检查 zipfile 是否正确 |
| -u | 更新文件，如有必要则创建文件 | -z | 仅显示压缩文件的注释 |
| -v | 执行时显示详细的信息 | -T | 更新时间戳到最新 |
| -j | 丢弃路径信息（不创建目录）| -a | 对文本文件进行必要的字符转换 |
| -U | 对于非 ASCII 字符做 unicode 转义 | -UU | 忽略全部 Unicode 字符 |
| -C | 对文件名称区分大小写 | -L | 将文件名称都转为小写 |
| -X | 还原 UID/GID 信息 | -V | 保留VMS的文件版本信息 |


## 使用实例

1. 解压文件到指定目录（test1）
    ``` bash
    gackle@machine:/Project$ unzip test.zip -d test1/
    ```


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