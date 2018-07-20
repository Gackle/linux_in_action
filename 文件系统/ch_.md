---
description: 修改文件权限命令集合
---

# chown 命令

`chown` 命令改变某个文件或目录的所有者和所属的组，该命令可以向某个用户授权，使该用户变成指定文件的所有者或者改变文件所属的组。

> 只有 **文件属主** 和 **超级用户(root)** 才可以使用该命令。


## 命令用法

``` shell
$ chown [OPTION]... [OWNER][:[GROUP]] FILE...
$ chown [OPTION]... --reference=RFILE FILE...
```

其中
- `OWNER` 代表要变更的文件属主，可以是用户或者是用户 ID
- `GROUP` 代表要变更的文件属组，可以是组名或组 ID
- `FILE` 可以是由空格分开的文件列表，在文件名中可以包含通配符

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| --reference=RFILE | 把指定文件或目录的拥有者与所属群组全部设成和参考文件或目录 `RFILE` 的拥有者与所属群组相同 |
| -R, --recursive | 递归处理，将指定目录下的所有文件及子目录一并处理 |
| -h, --no-dereference | 只对符号链接的文件作修改，而不更改其他任何相关文件 |
| -v, --verbose | 显示执行过程 |


## 使用实例

``` bash
# 将目录 /usr/gackle 及其下面的所有文件、子目录的文件属主改成 tim
$ chown -R tim /usr/gackle
```

# chgrp 命令
`chgrp` 命令用来改变文件或目录所属的用户组。该命令用来改变指定文件所属的用户组。

> 如果用户不是该文件的 **文件属主** 或 **超级用户(root)**，则不能改变该文件的组。


## 命令用法

``` shell
$ chgrp [OPTION]... GROUP FILE...
$ chgrp [OPTION]... --reference=RFILE FILE...
```

其中：
- `GROUP` 代表要变更的文件属组，可以是组名或组 ID
- `FILE` 可以是由空格分开的文件列表，在文件名中可以包含通配符

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| --reference=RFILE | 把指定文件或目录的拥有者与所属群组全部设成和参考文件或目录 `RFILE` 的拥有者与所属群组相同 |
| -R, --recursive | 递归处理，将指定目录下的所有文件及子目录一并处理 |
| -h, --no-dereference | 只对符号链接的文件作修改，而不更改其他任何相关文件 |
| -v, --verbose | 显示执行过程 |

## 使用实例

``` shell
# 将目录 /usr/meng 及其下面的所有文件、子目录的文件属组改成 staff
$ chgrp -hR staff /user/meng
```

# chmod 命令

`chmod` 命令用来变更文件或目录的权限。在 Linux 里，文件或目录权限的控制分别以<u>读取、写入、执行</u> 3 种一般权限来区分，另有 3 种特殊权限可供运用。用户可以使用 `chmod` 指令去变更文件与目录的权限，设置方式采用 **文字** 或 **数字代号** 皆可。

> <small>符号链接的权限无法变更，如果用户对符号链接修改权限，其改变会作用在被链接的原始文件。</small>

## 命令用法

``` shell
$ chmod [options]... mode[,mode ...] file[ file ...]
```

其中 `mode` 是下面形式的组合 `[ugoa]*([-+=]([rwxXst]*|[ugo]))+|[-+=][0-7]+`。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| --reference=RFILE | 把指定文件或目录的拥有者与所属群组全部设成和参考文件或目录 `RFILE` 的拥有者与所属群组相同 |
| -R, --recursive | 递归处理，将指定目录下的所有文件及子目录一并处理 |
| -v, --verbose | 显示执行过程 |

## 使用实例

1. 为文件设置属主可执行，同组成员可写入
``` shell
gackle@machine:~$ chmod u+x,g+w file
```

2. 为文件设置属主全权限，同组成员不可执行，其他用户只可读
``` bash
gackle@machine:~$ chmod u=rwx, g=rw, o=r file.txt

gackle@machine:~$ chmod 764 file.txt # 效果同上
```

3. 对文件设置为用户都有可执行权限
```
gackle@machine:~$ chmod a+x file
```