---
description: 密码管理命令集合
---

# passwd 命令

## 命令用法

``` shell
$ passwd [options] [LOGIN]
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -a, --all | report password status on all accounts
| -d, --delete | 删除密码，只有系统管理员可用 |
| -e, --expire | 强制密码过期 |
| -k, --keep-tokens | 设置为只有当密码过期后才能更新 |
| -l, --lock | 锁定密码 |
| -q, --quiet | 进入静默模式 |
| -S, --status | 出密码的相关信息，仅有系统管理者才能使用 |
| -u, --unlock | 解锁密码 |

# chage 命令

`chage` 命令用来帮助管理用户账户的有效期。

## 命令用法

``` shell
$  chage [options] LOGIN
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -d, --lastday LAST_DAY | 设置上次修改密码到现在的天数 |
| -E, --expiredate EXPIRE_DATE | 设置密码过期的日期 |
| -I, --inactive INACTIVE | 设置密码过期到锁定账户的天数 |
| -l, --list | 列出当前的设置，由非特权用户来确定他们的密码或帐号何时过期 |
| -m, --mindays MIN_DAYS | 密码保持有效的最小天数 |
| -M, --maxdays MAX_DAYS | 密码保持有效的最大天数 |
| -W, --warndays WARN_DAYS | 设置密码过期前多久开始出现提醒信息 |

> 注意，这里的日期格式有两种：  
>
> - YYYY-MM-DD 格式的日期 
> - 代表从1970年1月1日起到该日期天数的数值 

# chpasswd 命令

`chpasswd` 命令是批量更新用户口令的工具，是把一个文件内容重新定向添加到 **/etc/shadow** 中。

## 命令用法

``` shell
$ chpasswd [options]
```

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -c, --crypt-method METHOD | 指定密码加密方法，`METHOD` 可以是 （NONE DES MD5 SHA256 SHA512） 其中之一 |
| -e, --encrypted | 输入的密码是加密后的密文 |
| -m, --md5 | 当被支持的密码未被加密时，使用 MD5 加密代替 DES 加密 |
| -s, --sha-rounds | 指定 SHA 加密算法的位数 |
