---
description: umask 命令 —— 设置限制新建文件权限的掩码
---
# umask 命令

其实在 Linux 中 `umask` 命令更像是属于权限管理部分的命令。`umask` 命令用来<u>设置限制新建文件权限的掩码</u>。当新文件被创建时，其最初的权限由文件创建掩码决定。

用户每次注册进入系统时，`umask` 命令都被执行， 并自动设置掩码 **mode** 来限制新文件的权限。

用户可以通过再次执行 `umask` 命令来改变默认值，新的权限将会把旧的覆盖掉。

## 命令用法
``` shell
$ umask [-p] [-S] [mode]
```

利用 `umask` 命令可以 **指定哪些权限将在新文件的默认权限中被删除**。例如，可以使用下面的命令创建掩码，使得组用户的写权限，其他用户的读、写和执行权限都被取消：

``` shell
gackel@machine:~$ umask u=, g=w, o=rwx
```


`umask` 不带 `mode` 参数是显示这个默认的权限。如果 `mode` 参数是以数字开头，那么它会被认为是八进制数的[文件权限码](README.md#authorization-number)进行解析；否则它必须是以[文件权限符](README.md#authorization-symbolic)的字符串形式给出(即 `u=rwx, g=rwx, o=rwx`)。其中两个可选项：
- `-p`：如果 `mode` 参数缺失，则输出的权限掩码可直接作为指令来执行；
- `-S`：以[文件权限符](README.md#authorization-symbolic)的形式输出权限掩码（默认是以八进制数的[文件权限码](README.md#authorization-number)输出）。