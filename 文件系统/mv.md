---
description: mv 命令 —— 重命名文件
---
# mv 命令

在 Linux 中，重命名文件称为**移动（moving）**。`mv` 命令可以将文件和目录移动到另一个位置或重新命名。 

## 命令用法

``` shell
$ mv [OPTION] source destination
```

注意，`mv` 命令只会影响文件名而不会影响 inode 编号和时间戳。

## 常用可选参数 ##

| 选项 | 说明 |
|:---|:---|
| -f | （destination 已存在，）使用强制（force）覆盖，若 destination 已经存在且无法开启，则移除之后再尝试一次（使用 -n 时该命令无效） |
| -i | （destination 已存在，）覆盖前提示 |
| -n | （destination 已存在，）不允许覆盖 |
| -b | 覆盖已存在的 destination 前将 destination 备份 |
| -u | 当且仅当 source 的日期比 destination 新或者 destination 不存在时才会移动/重命名 |