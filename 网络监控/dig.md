---
description: dig 命令 —— 域名查询工具
---

# dig 命令

`dig` 命令是常用的域名查询工具，可以用来测试域名系统工作是否正常。

## 命令用法

``` shell
$ dig [@global-server] [domain] [q-type] [q-class] {q-opt}  {global-d-opt} host [@local-server] {local-d-opt} [ host [@local-server] {local-d-opt} [...]]
```

其中：
- @global-server：  可选，指定进行域名解析的域名服务器，`global-server` 为服务器地址
- q-type：          可选，指定DNS查询的类型，可以是 (`in`,`hs`,`ch`,...) 中的任何一个，默认是 `in`
- q-class：         可选，指定查询 DNS 的 class，可以是 (`a`,`any`,`mx`,`ns`,`soa`,`hinfo`,`axfr`,`txt`,...) 中的任何一个，默认是 `a`
- q-opt：           可选，指定查询的选项
- d-opt：           可选，指定查询的选项
- host：            必填，需要查询的域名

## 常用可选参数

1. q-opt
    | 参数 | 说明 |
    |:---|:---|
    | -4 | 只使用 IPv4 查询 |
    | -6 | 只使用 IPv6 查询 |
    | -b address [#port] | 绑定源地址/端口 |
    | -c class | 指定查询的 DNS class |
    | -t type | 指定查询的 DNS 类型 | 
2. d-opt
    | 参数 | 说明 |
    |:---|:---|
    | +[no]dnssec | 请求 DNSSEC 记录|
    | +[no]trace | 跟踪查询 DNS 过程 |


## 参数解析 

``` shell
gackle@machine:~$ dig www.baidu.com

; <<>> DiG 9.11.2-P1-1-Debian <<>> +all www.scnu.edu.cn
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62380
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags: do; udp: 4000
;; QUESTION SECTION:
;www.scnu.edu.cn.               IN      A

;; ANSWER SECTION:
www.scnu.edu.cn.        605     IN      A       121.8.171.26

;; Query time: 2 msec
;; SERVER: 202.96.128.86#53(202.96.128.86)
;; WHEN: Thu Jul 19 16:44:47 DST 2018
;; MSG SIZE  rcvd: 60
```

开头是一些统计信息，可以不用管，具体看 `SECTOIN` 部分：

- `QUESTION SECTION`: 提问环节，显示你要查询的域名
- `ANSWER SECTION`：答案环节，显示查询到的域名对应的 IP
- 最后面的是一些统计信息，其中 `SERVER` 指的是直接为你服务的本地 DNS 服务器的 IP。

> <small> 这里 605 代表 ttl（time to live， 暂存时间），表示这次请求会在服务器上保存多久时间（单位：秒）；`IN` 是固定关键词；`A` 代表 A 类型的 DNS 记录。</small>