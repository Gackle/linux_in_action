---
description: 文件查找命令集合 
---
# find 命令

`find` 命令用来在指定目录下查找文件。任何位于参数之前的字符串都将被视为欲查找的目录名。

## 命令用法

``` shell
$ find [-path...] -options [-print -exec -ok] 
```

如果使用该命令时，不设置任何参数，则 `find` 命令将在当前目录下查找子目录与文件。并且将查找到的子目录和文件全部进行显示。

其中:

- `path`： 要查找的目录路径
    - `~` 代表 `$HOME` 目录
    - `.` 代表当前目录
    - `/` 代表根目录
- `print`： 表示将结果输出到标准输出
- `exec`： 对匹配的文件执行该参数所给出的 shell 命令，形式为 `command {} \;`，注意 `{}` 和 `\;` 之间有空格
- `ok`：和 `exec` 作用相同，区别在于，再执行命令前都会给出提示，让用户确认是否执行。

## 常用可选参数 

| 参数 | 说明 |
|:---|:---|
| -name NAME | 按名字 `NAME` 查找 |
| -perm PERM | 按权限 `PERM` (八进制数 777)查找 |
| -prune |不寻找字符串作为寻找文件或目录的范本样式 |
| -user | 按文件属主来查找 |
| -group | 按文件所属群组来查找 |
| -nogroup | 查找无有效所属群组的文件 |
| -nouser | 查找无有效属主的文件 |
| -maxdepth | 基于目录深度查找，向下最大深度限制 |
| [时间戳单位] [+/-] NUM  | 时间戳取值为 `-[a|m|c][time|min]`，a、m、c 分别代表访问时间、修改时间和变化时间，time 表示天而 min 表示分钟。 `+` 表示 `NUM` 个时间戳单位前，`-` 表示 `NUM` 个时间单位之内。|
| -type TYPE | 按文件类型 `TYPE` 来查找，`f` 代表普通文件, `l` 代表符号链接，`d` 代表目录， `c` 代表字符设备，`b` 代表块设备，`s` 代表套接字，`p` 代表 Fifo |
| -empty | 寻找文件大小为 0 Byte 的文件，或目录下没有任何子目录或文件的空目录 |
| -follow | 排除符号链接 |
| -size SIZE | 按文件大小 `SIZE` 来查找，`b` 代表块（512字节），`c` 代表字节，`w` 代表字（2 字节），`k` 代表千字节，`M` 代表兆字节，`G` 代表吉字节 |
| -o | 连接两个不同的条件(两个条件只要满足一个即可) |

## 使用实例

1. 按名字查找
    - 在 /etc 目录及其子目录下查找 host 开头的文件
        ``` shell
        $ find /etc -name 'host*' -print
        ```
    - 在当前目录或子目录中，查找不是 out 开头的 txt 文件
        ``` shell
        $ find . -name "out*" -prune -o -name "*.txt" -print
        $ find . -name ! "out*" -o -name "*.txt" -print
        ```
2. 按目录查找：
    - 在当前目录而不在子目录中查找 txt 文件
        ``` bash
        $ find . ! -name "." -type d -prune -o -type f -name "*.txt" -print
        ```
3. 按权限查找：
    - 在当前目录以及子目录中查找属主具有全部权限，其他具有执行权限的文件：
        ``` shell
        $ find . -perm 755 -print
        ```
4. 按时间查找：
    - 查找 2 天内被更改过的文件：
        ``` shell
        $ find . -mtime -2 -type f -print
        ```
    - 查找一天前被访问过的文件：
        ``` shell
        $ find . -atime +1 -type f -print 
        ```
    - 查找 10 分钟前状态被修改过的文件：
        ``` shell
        $ find . -cmin +10 -type f -print
        ```
5. 按大小查找：
    - 查找大于 1 M 的文件：
        ``` bash
        $ find . -size +1M -type f -print
        ```
    - 查找等于 6 字节的文件：
        ``` bash
        $ find . -size 6c -print
        ```
    - 查找小于 32 K 的文件：
        ``` bash
        $ find . -size 32k -print
        ```
6. 按文件新旧查找：
    - 查找比 aa.txt 新的文件
        ``` shell
        $ find . -newer "aa.txt" -type f -print
        ```
7. 列出长度为 0 的文件：
    ``` shell
    $ find . -empty --exec ls {} \;
    ```
8. 删除临时文件:
    ``` shell
    $ find . \(-name a.out -o -name '*.o' -o -name 'core'\) --exec rm {} \;
    ```

# which 命令
`which` 命令用于查找并显示给定**命令**的绝对路径，环境变量 PATH 中保存了查找命令时需要遍历的目录。

`which` 指令会在环境变量 `$PATH` 设置的目录里查找符合条件的文件。也就是说，使用 `which` 命令，就可以看到某个系统命令是否存在，以及执行的到底是哪一个位置的命令。

## 命令用法

``` shell
$ which [-a] filenames ...
```

## 使用实例

``` shell
gackle@machine:~$ which pwd useradd
/bin/pwd
/usr/sbin/useradd
```

# whereis 命令

`whereis` 命令用来定位指令的二进制程序、源代码文件和 man 手册页等相关文件的路径。

`whereis` 命令只能用于程序名的搜索，而且只搜索二进制文件（参数 `-b` ）、man 说明文件（参数 `-m` ）和源代码文件（参数 `-s` ）。如果省略参数，则返回所有信息。

## 命令用法

``` shell
$ whereis [options] [-BMS <dir>... -f] <name>
```

## 可选参数列表
| 参数 | 说明 |
|:---|:---|
| -b | 只查找二进制文件 |
| -B \<dirs\> | 定义二进制文件的查找路径 |
| -m | 只查找 man 说明文件 |
| -M \<dirs\> | 定义 man 说明文件的查找路径 |
| -s | 只查找源代码文件 |
| -S \<dirs\> | 定义源代码文件的查找路径 |
| -u | 查找不包含指定类型的文件 |
| -f | 不显示文件名前的路径名称 |
| -l | 输出有效的查找路径 |


## 使用实例

``` shell
gackle@machine:~$ whereis stdio.h
stdio: /usr/include/stdio.h /usr/share/man/man3/stdio.3.gz
gackle@machine:~$ whereis -b stdio.h
stdio: /usr/include/stdio.h
gackle@machine:~$ whereis -m stdio.h
stdio: /usr/share/man/man3/stdio.3.gz
gackle@machine:~$ whereis -s stdio.h
stdio:
gackle@machine:~$ whereis -f stdio.h
stdio: /usr/include/stdio.h /usr/share/man/man3/stdio.3.gz
```

## whereis 高效的原因以及缺陷

和 `find` 相比，`whereis` 查找的速度非常快，<u>这是因为 Linux 系统会将系统内的所有文件都记录在一个数据库文件中</u>，当使用 `whereis` (`locate` 也同样)时，会从数据库中查找数据，而不是像 `find` 命令那样，通过遍历硬盘来查找，效率自然会很高。 但是该数据库文件并不是实时更新，默认情况下时一星期更新一次，因此，我们在用 `whereis` 和 `locate` 查找文件时，有时会找到已经被删除的数据，或者刚刚建立文件，却无法查找到，原因就是因为数据库文件没有被更新。


# locate 命令

`locate` 命令其实是 `find -name` 的另一种写法，但是要比后者快得多，原因在于它不搜索具体目录，而是搜索一个数据库 **/var/lib/locatedb**，这个数据库中含有本地所有文件信息。<u>Linux 系统自动创建这个数据库，并且每天自动更新一次，所以使用`locate` 命令查不到最新变动过的文件</u>。为了避免这种情况，可以在使用 `locate` 之前，先使用 `updatedb` 命令，手动更新数据库。 

## 命令用法

``` bash
$ locate [OPTIONs] [PATTERNs]
```

## 常用可选参数
| 参数 | 说明 |
|:---|:---|
| -c, --count | 只显示匹配 pattern 的文件或目录数目 |
| -d, --database DBPATH | 使用指定 `DBPATH` 的数据库路径而不是默认的 `/var/lib/mlocate/mlocate.db` |
| -e, --existing | 只显示当前存在的文件 |
| -l, --limit, -n LIMIT | 限制显示 `LIMIT` 条匹配记录 |
| -r, --regexp, --regex REGEXP | 不采用模式匹配而是使用 `REGEXP` 的正则表达式匹配 |