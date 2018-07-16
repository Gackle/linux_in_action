---
description: cp 命令 —— 复制文件
---

# cp 命令

`cp` 命令负责在文件系统中将文件和目录从一个位置复制到另一个位置。

## 命令用法 ##

``` shell
$ cp [OPTION] source destination 
```

当 source 和 destination 参数都是文件名时，`cp` 命令将源文件复制成一个新文件，并且以 destination 命名。新文件就像全新的文件一样，有新的修改时间。 

## 常用可选选项

| 选项 | 说明 |
|:---|:---|
| -f | （destination 已存在，）使用强制（force）覆盖，若 destination 已经存在且无法开启，则移除之后再尝试一次（使用 -n 时该命令无效） |
| -i | （destination 已存在，）覆盖前提示 |
| -n | （destination 已存在，）不允许覆盖 |
| -R, -r | 如果目标路径的所在的目录不存在，递归创建目录 |
| -d | 如果 source 为符号连接 link 时，destination 也建立为符号连接，并指向与 source 的原始文件或目录 |
| -l | destination 建立的是 source 的硬连接而非拷贝 |
| -s | destination 建立的是 source 的符号连接而非拷贝 |
| -b | 覆盖已存在的 destination 前将 destination 备份 |
| -p | 保留 source 的属性 |
| -a | 相当于 -dpR |
| -u | 当且仅当 source 的日期比 destination 新或者 destination 不存在时才会复制 |