---
description: scp 命令 —— 跨机远程拷贝
---

# scp 命令

`scp` 是 *secure copy* 的缩写，是用于在 Linux 下进行远程拷贝文件的命令，是基于 ssh 登陆的加密传输。

> `scp` 和 `cp` 一样是拷贝文件，不过后者是用于本机拷贝的命令；`rcp` 则是用于跨机拷贝，不过是非加密的；`rsync` 和 `scp` 的功能一样，不过后者消耗资源少，不会提高系统负荷，前者会更快一些不过在小文件多的情况下会导致磁盘 I/O 非常高。

## 命令用法

``` shell
scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
    [-l limit] [-o ssh_option] [-P port] [-S program]
    [[user@]host1:]file1 ... [[user@]host2:]file2
# scp [参数] 源路径 目标路径
```

## 常用可选参数 

| 参数 | 说明 |
|:---|:---|
| -3 | 通过本机在两台远程主机上进行拷贝，如果没有这个选项则会直接拷贝到两个远程主机上。此选项会禁用进度条 |
| -4 | 强制 `scp` 使用 IPv4 寻址 |
| -6 | 强制 `scp` 使用 IPv6 寻址 |
| -B | 使用批处理模式（传输过程中不再询问密码或 passphrases 短语 |
| -C | 允许压缩（此 `-C` flag 会直接传递给 `ssh`） |
| -c cipher | 选择加密传输的算法，此 flag 会直接传递给 `ssh` |
| -F ssh_config | 为每个用户指定独立的 `ssh` 配置文件 |
| -i identity_file | 指定要从哪里读取对应公钥的私钥身份标识，此 flag 会直接传递给 `ssh` |
| -l limit | 限定用户所能使用的带宽，以 **Kbit/s** 为单位 |
| -P port | 指定要连接远端主机的端口号；注意是大写的 *P* 因为 `-p` 已经用于保留文件的时间（修改时间、访问时间）和 mode 模式 |
| -p | 保留源文件的修改时间、访问时间以及 mode 模式 |
| -q | 开启静默模式 |
| -r | 递归复制整个目录 |
| -v | 详细模式显示输出，`scp` 和 `ssh` 都会显示整个过程的调试信息，用于调试连接、验证和配置问题 |


## 使用实例

1. 从本地服务器复制到远端服务器

    ``` shell
    $ scp -r /opt/project root@10.117.227.124:/opt/project
    ```
2. 从远端服务器复制文件到本地

    ```shell
    $ scp -r root@10.6.159.147:/opt/soft/demo.tar /opt/soft/
    ```
