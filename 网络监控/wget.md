---
description: wget 命令 —— 从指定的 URL 下载文件
---

# wget 命令

根据帮助信息可知，`wget` 是一个 GNU 提供的非交互式的网络接收器工具。

`wget` 非常稳定，它在带宽很窄的情况下和不稳定网络中有很强的适应性，如果是由于网络的原因下载失败， `wget` 会不断的尝试，直到整个文件下载完毕。如果是服务器打断下载过程，它会再次联到服务器上从停止的地方继续下载。这对从那些限定了链接时间的服务器上下载大文件非常有用。

## 命令用法 

``` bash
$ Usage: wget [OPTION]... [URL]...
```

## 常用可选参数

虽然 `wget` 是非交互式的工具，但由于它提供了多种参数，所以功能依然非常强大。这里仅列出部分常用参数。

### 1. 启动项参数

| 参数 | 说明 |
|:---|:---|
| -V, --version | 显示 wget 的版本信息并退出 |
| -b, --background | 启动 wget 之后切换到后台运行 |

### 2. 日志和输入文件参数

| 参数 | 说明 |
|:---|:---|
| -o, --output-file=FILE | 在 `FILE` 文件中记录日志信息 |
| -a, --append-output=FILE | 在 `FILE` 文件中追加日志信息 |
| -d, --debug | 显示大量 debug 信息 |
| -q, --quiet | 使用静默模式 |
| -v, --verbose | 显示执行过程信息（默认开启） |
| -i, --input-file=FILE | 从本地或外部文件中下载找到的 URL 信息 |
| -F, --fore-html | 将输入文件当作 HTML 来处理 |

### 3. 下载选项参数 

| 参数 | 说明 |
|:---|:---|
| -t, --tries=NUMBER | 设置重复次数（0 代表无限次）|
| -O, --output-document=FILE | 输出文件内容到 `FILE` 文件上 |
| -c, --continue | 从一个部分下载文件中恢复下载 |
| -S, --server-response | 显示服务器应答信息 |
| --spider | 不下载任何东西 |
| -T, --timeout=SECONDS | 设置全部的超时时间值为 `SECONDS`，可以分别单独设置 dns-timeout、connect-timeout 以及 read-timeout |
| -w, --wait=SECONDS | 重试之前需要等待 `SECONDS` 秒 |
| --limit-rate=RATE | 限制下载速度为 `RATE` |
| --user=USER | 设置 ftp 或 http 登陆用户为 `USER` |
| --password=PASS | 设置 ftp 或 http 登陆密码为 `PASS` |
| --ask-password | 以提示符 prompt 的形式输入密码 |
| --no-iri | 关闭iri(国际化资源标识符)支持 |
| --local-encoding=ENC | 对 IRI 以 `ENC` 作为本地编码 |
| --remote-encoding=ENC | 使用 `ENC` 作为远端的默认编码 |

### 4. 目录参数

| 参数 | 说明 |
|:---|:---|
| -nd, --no-directories | 不创建目录 |
| -x, --force-directories | 强制要求创建目录 |
| -P, --directory-prefix=PREFIX | 存储文件到 `PREFIX/..` 目录下 |

### 5. HTTP 选项参数

| 参数 | 说明 |
|:---|:---|
| --http-user=USER | 设置 http 登陆用户为 `USER` |
| --http-password=PASS | 设置 http 登陆密码为 `PASS` |
| --no-cache | 不允许服务器缓存数据 |
| --max-redirect | 设置每一个页面的最大重定向次数 |
| --referer=URL | 设置 referer 头 |
| --save-headers | 保存 HTTP 请求头到文件中 |
| -U, --user-agent=AGENT | 指定 user-agent 而不是使用默认的 `Wget/VERSION` |
| --no-http-keep-alive | 不使用 HTTP 长连接 |
| --no-cookis | 不使用 cookies |
| --load-cookies=FILE | 会话开始前从 `FILE` 中读取 cookie |
| --save-cookies=FILE | 会话开始后将 cookie 保存到 `FILE` |
| --keep-session-cookies | 读取并保存会话（非永久）的 cookies |
| --post-data=STRING | 使用 POST 方法，发送 `STRING` 作为数据 |
| --post-file=FILE | 使用 POST 方法，发送 `FILE` 的内容作为数据 |
| --method=HTTPMethod | 指定使用的 HTTP 方法 |
| --body-data=STRING | 发送 `STRING` 作为数据 —— `method` 参数必须设置 |
| --body-file=FILE | 发送文件 `FILE` 的内容 —— `method` 参数必须设置 |

### 6. HTTPS (SSL/TLS) 参数 

| 参数 | 说明 |
|:---|:---|
| --no-check-certificate | 不校验服务器的证书 |

### 7. FTP 参数 

| 参数 | 说明 |
|:---|:---|
| --ftp-user=USER | 设置 ftp 用户为 `USER` |
| --ftp-password=PASS | 设置 ftp 密码为 `PASS` |
| --preserve-permissions | 暂存远程文件的权限 |

### 8. 循环下载

| 参数 | 说明 |
|:---|:---|
| -r, --recursive | 指明使用递归下载方式方式 |
| -l, --level=NUMBER | 指定最大递归深度（`inf` 或 0 代表无限递归） |

## 使用实例

### 1. wget 限速下载 

``` bash
$ wget https://codeload.github.com/dotnetcore/EasyCaching/zip/master -O EasyCaching.zip --limit-rate=2k
--2018-09-17 17:59:39--  https://codeload.github.com/dotnetcore/EasyCaching/zip/master
Resolving codeload.github.com (codeload.github.com)... 192.30.253.120, 192.30.253.121
Connecting to codeload.github.com (codeload.github.com)|192.30.253.120|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/zip]
Saving to: ‘EasyCaching.zip’

EasyCaching.zip                   [               <=>                                ]  83.48K  2.00KB/s
```

### 2. wget 后台下载

``` bash
$ wget -b https://codeload.github.com/dotnetcore/EasyCaching/zip/master -O EasyCaching.zip
Continuing in background, pid 66.
Output will be written to ‘wget-log’.
$ ls
EasyCaching.zip
```

### 3. 测试下载链接是否有效

``` bash
$ wget --spider [url]
```

### 4. 以不同文件名保存

``` bash
$  wget -b https://codeload.github.com/dotnetcore/EasyCaching/zip/master -O EasyCaching.zip
Continuing in background, pid 66.
Output will be written to ‘wget-log’.
```

### 5. 保存下载日志

``` bash
$ wget -o download.log [url]
```

### 6. 断点续传

``` bash
$ wget https://codeload.github.com/dotnetcore/EasyCaching/zip/master -O EasyCaching.zip --limit-rate=4k
[中断网路]
$ wget -c https://codeload.github.com/dotnetcore/EasyCaching/zip/master -O EasyCaching.zip 
```