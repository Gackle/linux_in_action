----
description: 查看 Linux 内核和系统信息
----

# 查看内核信息

## 1. 查看 /proc/version 文件

``` shell
$ cat /proc/version
Linux version 4.4.0-17134-Microsoft (Microsoft@Microsoft.com) (gcc version 5.4.0 (GCC) ) #137-Microsoft Thu Jun 14 18:46:00 PST 2018
```

## 2. 使用 uname 命令

### 命令用法 

``` bash
uname [OPTION]...
```

### 常用可选参数

| 参数 | 说明 |
|:---:|:---|
| -a, --all | 打印全部信息，顺序如同下面依次介绍的顺序（特殊情况下会忽略 -p 和 -i），以空格隔开|
| -s, --kernel-name | 打印内核名称 |
| -n, --nodename | 打印在网络中机器节点的 host 名称 |
| -r, --kernel-release | 打印内核发行版本 |
| -v, --kernel-version | 打印内核版本 |
| -m, --machine | 打印机器硬件名 |
| -p, --processor | 打印处理器类型信息 |
| -i, --hardware-platform | 打印硬件平台信息 |
| -o, --operating-system | 打印操作系统信息 |

### 常用用法

``` shell
$ uname -a 
Linux DESKTOP-8NBNTP3 4.4.0-17134-Microsoft #137-Microsoft Thu Jun 14 18:46:00 PST 2018 x86_64 x86_64 x86_64 GNU/Linux
```

# 查看系统信息

## 1. 查看 /etc/issue 文件

``` bash
$ cat /etc/issue
Ubuntu 16.04.5 LTS \n \l

```

## 2. 使用 lsb_release 工具

Linux 里的 `lsb_release` 命令用来查看当前系统的发行版信息（prints certain LSB (Linux Standard Base) and Distribution information.）

> 注意，有些系统不一定安装了这个命令，如有必要可以使用上面的方法。

### 命令用法 

``` shell
lsb_release [options]
```

### 常用可选参数

| 参数 | 说明 |
|:---:|:---|
| -v, --version | 显示系统支持的 LSB 模块 |
| -i, --id | 显示发行方 ID |
| -d, --description | 显示发行版本的描述 |
| -r, --release | 显示发行版本的发行号 |
| -c, --codename | 显示发行版本的 codename |
| -a, --all | 显示上述所有信息 |
| -s, --short | 以简短形式显示所请求的信息 |

### 使用实例 

``` bash
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.5 LTS
Release:        16.04
Codename:       xenial
```
