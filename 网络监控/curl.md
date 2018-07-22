---
description: curl 命令 —— 利用URL语法在命令行方式下工作的开源文件传输工具
---

# curl 命令

`curl` 命令是一个利用URL规则在命令行下工作的文件传输工具。它支持文件的上传和下载，所以是综合传输工具，但按传统，习惯称 `curl` 为下载工具。作为一款强力工具，`curl` 支持包括HTTP、HTTPS、ftp 等众多协议，还支持 POST、cookies、认证、从指定偏移处下载部分文件、用户代理字符串、限速、文件大小、进度条等特征。

# 命令用法

``` shell
$ curl [options]... <url>
```

注意 `url` 请求地址最好用 `""` 括起来。

`curl` 是将下载文件输出到 stdout，将进度信息输出到 stderr，不显示进度信息使用 `--silent` 选项。

## 常用可选参数

| 参数 | 说明 |
|:---|:---|
| -A, --user-agent STRING | 设置用户代理报头信息 `STRING` 发送给服务器 |
| -b, --cookie DATA | 设置 cookie 的数据 `DATA`，可以是字符串或文件的读取位置 |
| -c, --cookie-jar FILE | 操作结束后把 cookie 写入这个文件 `FILE` 中 |
| -d, --data DATA/@FILE | HTTP POST 方式传送数据 `DATA` 或者 `FILE` 文件的内容 |
| --data-ascii DATA | 以 ascii 的方式 post 数据 `DATA` |
| --data-binary DATA | 以二进制的方式 post 数据 `DATA` |
| -D, --dump-header FILE | 将响应报头信息写到 `FILE` 文件中 |
| -F, --form NAME=CONTENT | 提交 multipart MIME 数据，以 `NAME=CONTENT` 的形式 |
| --form-string NAME=STRING | 提交 multipart MIME 数据，以 `NAME=STRING` 的形式 |
| -e, --referer URL | 指定来源网址 `URL` |
| -H, --header LINE/@FILE | 自定义报头信息 `LINE` 或 `FILE` 文件的内容作为报头信息传递给服务器 |
| --ignore-content-length | 忽略 HTTP 头信息的长度 |
| -Q, --quote COMMAND | 文件传输前，发送命令 `COMMAND` 到服务器 |
| -o, --output FILE | 把输出写到该文件 `FILE` 中 |
| -O, --remote-name | 把输出写到文件中，并保留远程文件名 |
| --limit-rate RATE | 限制下载速度为 `RATE` |
| -u, --user USER[:PASSWORD] | 设置服务器的用户和密码 |
| -U, --proxy-user USER[:PASSWORD] | 设置代理用户名和密码 |
| -x, --proxy HOST[:PORT] | 设置代理 `HOST` 地址 |
| -X, --request COMMAND | 指定使用什么命令 `COMMAND` |

## 使用实例

1. 下载文件：
    - 下载单个文件，默认将输出打印到 stdout 中：
        ``` shell
        $ curl http://www.centos.org/
        ```
    - 下载到指定文件中：
        ``` shell
        curl -o mygettext.html http://www.gnu.org/software/gettext/manual/gettext.html

        curl -O http://www.gnu.org/software/gettext/manual/gettext.html
        ```
    - 对 `curl` 的最大网络使用进行限制：
        ``` shell
        $ curl --limit-rate 1000B -O http://gnu.org/software/gettext/manual/gettext.html
        ```
    - 从 FTP 服务器上下载所有文件：
        ``` shell
        $ curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/
        ```
2. 保存于使用网站 cookie 信息
    - 将 cookies 保存到 sugercookies 文件中
        ``` shell
        $ curl -D sugercookies http://localhost/sugercrm/index
        ```
    - 使用 sugercookies 保存的 cookies
        ``` shell
        $ curl -b sugercookies http://localhost/sugercrm/login
        ```
3. 传递请求数据
    - 使用 GET 方法请求数据
        ``` shell
        $ curl -u username https://api.github.com/user?access_token=XXXXX
        ```
    - 使用 POST 方法请求数据
        ```shell
        $ curl --data "param1=value1&param2=value" http://api.github.com/

        $ curl --data @data.json http://api.github.com/authorizations
        ```
    - 自动转义参数中的特殊字符
        ``` shell
        $ curl --data-urlencode "value 1" http://hostname.com 
        ```
    - 使用其他方法请求
        ``` shell
        $ curl -X DELETE https://api.github.com
        ```
    - 设置 http 请求头：
        ``` shell
        $ curl -A "Mozilla/5.0 Firefox/21.0" http://www.baidu.com #设置 http 请求头 User-Agent

        $ curl -H "Content-Type: application/json \n Connection: keep-alive" http://www.aiezu.com
        ```
    - 设置 http 响应头
        ``` shell
        $ curl -I http://www.aiezu.com # 仅返回 header

        $ curl -D /tmp/header http://www.aiezu.com # 将 http header 保存到 /tmp/header 文件
        ```
4. 上传文件
    - 同时上传多个文件到 FTP 服务器
        ``` shell
        $ curl -u ftpuser:ftppass -T "{file1, file2}" ftp：//ftp.testserver.com
        ```
    - 从标准输入获取内容保存到 FTP 服务器指定的文件中
        ``` shell
        $ curl -u ftpuser:ftppass -T ftp://ftp.testserver.com/myfile.txt
        ```
    - 以表单数据的形式上传文件
        ```shell
        $ curl --form "fileupload=@filename.txt" http://hostname/resource
        ```
5. 其他设置
    - 为 `curl` 设置代理
        ``` shell
        $ curl -x proxyserver.test.com:3128 http://google.com
        ```
    - 显示一次 HTTP 请求的通信过程
        ``` shell
        $ curl -v http://www.baidu.com
        ```
    - 跟随重定向的链接
        ```shell
        $ curl -L http://codebelief.com
        ```