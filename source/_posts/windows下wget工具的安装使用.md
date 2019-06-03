---
title: windows下wget工具的安装使用
date: 2019-05-27 11:11:12
top: true
categories: 工具
tags: [工具]
---
# windows下wget工具的安装使用

<a name="pRZoz"></a>
# 前言
GNU Wget是一个在网络上进行下载的简单而强大的自由软件，其本身也是GNU计划的一部分。它的名字是“World Wide Web”和“Get”的结合，同时也隐含了软件的主要功能。目前它支持通过HTTP、HTTPS，以及FTP这三个最常见的TCP/IP协议协议下载。
<a name="oC5mQ"></a>
## 特点：
1）支持断点下传功能<br />2）同时支持FTP和HTTP下载方式<br />3）支持代理服务器<br />4）设置方便简单；<br />5）程序小，完全免费；
<a name="joBjO"></a>
##  缺点
1）支持的协议较少，特别是cURL相比。流行的流媒体协议mms和rtsp没有得到支持，还有广泛使用各种的P2P协议也没有涉及。<br />2）支持协议过老。目前HTTP还是使用1.0版本，而HTML中通过JavaScript和CSS引用的文件不能下载。<br />3）灵活性不强，扩展性不高。面对复杂的镜像站会出现问题。<br />4）命令过于复杂，可选的设置项有上百个。<br />5）安全问题
<a name="z25P6"></a>
# 下载
下载地址: [https://eternallybored.org/misc/wget/](https://eternallybored.org/misc/wget/)
<a name="aKhEz"></a>
# 安装步骤

1. 从上述地址中下载最新版的exe文件
1. 把wget.exe复制到C:\Windows\System32。
1. 在终端输入wget --help 查看

```powershell
λ wget --help
GNU Wget 1.20.3, a non-interactive network retriever.
Usage: wget [OPTION]... [URL]...

Mandatory arguments to long options are mandatory for short options too.

Startup:
  -V,  --version                   display the version of Wget and exit
  -h,  --help                      print this help
  -b,  --background                go to background after startup
  -e,  --execute=COMMAND           execute a `.wgetrc'-style command

Logging and input file:
  -o,  --output-file=FILE          log messages to FILE
  -a,  --append-output=FILE        append messages to FILE
  -d,  --debug                     print lots of debugging information
  -q,  --quiet                     quiet (no output)
  -v,  --verbose                   be verbose (this is the default)
  -nv, --no-verbose                turn off verboseness, without being quiet
       --report-speed=TYPE         output bandwidth as TYPE.  TYPE can be bits
  -i,  --input-file=FILE           download URLs found in local or external FILE
       --input-metalink=FILE       download files covered in local Metalink FILE
  -F,  --force-html                treat input file as HTML
  -B,  --base=URL                  resolves HTML input-file links (-i -F)
                                     relative to URL
       --config=FILE               specify config file to use
       --no-config                 do not read any config file
       --rejected-log=FILE         log reasons for URL rejection to FILE

Download:
  -t,  --tries=NUMBER              set number of retries to NUMBER (0 unlimits)
       --retry-connrefused         retry even if connection is refused
       --retry-on-http-error=ERRORS    comma-separated list of HTTP errors to retry
  -O,  --output-document=FILE      write documents to FILE
  -nc, --no-clobber                skip downloads that would download to
                                     existing files (overwriting them)
       --no-netrc                  don't try to obtain credentials from .netrc
  -c,  --continue                  resume getting a partially-downloaded file
       --start-pos=OFFSET          start downloading from zero-based position OFFSET
       --progress=TYPE             select progress gauge type
       --show-progress             display the progress bar in any verbosity mode
  -N,  --timestamping              don't re-retrieve files unless newer than
                                     local
       --no-if-modified-since      don't use conditional if-modified-since get
                                     requests in timestamping mode
       --no-use-server-timestamps  don't set the local file's timestamp by
                                     the one on the server
  -S,  --server-response           print server response
       --spider                    don't download anything
  -T,  --timeout=SECONDS           set all timeout values to SECONDS
       --dns-timeout=SECS          set the DNS lookup timeout to SECS
       --connect-timeout=SECS      set the connect timeout to SECS
       --read-timeout=SECS         set the read timeout to SECS
  -w,  --wait=SECONDS              wait SECONDS between retrievals
       --waitretry=SECONDS         wait 1..SECONDS between retries of a retrieval
       --random-wait               wait from 0.5*WAIT...1.5*WAIT secs between retrievals

       --no-proxy                  explicitly turn off proxy
  -Q,  --quota=NUMBER              set retrieval quota to NUMBER
       --bind-address=ADDRESS      bind to ADDRESS (hostname or IP) on local host
       --limit-rate=RATE           limit download rate to RATE
       --no-dns-cache              disable caching DNS lookups
       --restrict-file-names=OS    restrict chars in file names to ones OS allows
       --ignore-case               ignore case when matching files/directories
  -4,  --inet4-only                connect only to IPv4 addresses
  -6,  --inet6-only                connect only to IPv6 addresses
       --prefer-family=FAMILY      connect first to addresses of specified family,
                                     one of IPv6, IPv4, or none
       --user=USER                 set both ftp and http user to USER
       --password=PASS             set both ftp and http password to PASS
       --ask-password              prompt for passwords
       --use-askpass=COMMAND       specify credential handler for requesting
                                     username and password.  If no COMMAND is
                                     specified the WGET_ASKPASS or the SSH_ASKPASS
                                     environment variable is used.
       --no-iri                    turn off IRI support
       --local-encoding=ENC        use ENC as the local encoding for IRIs
       --remote-encoding=ENC       use ENC as the default remote encoding
       --unlink                    remove file before clobber
       --keep-badhash              keep files with checksum mismatch (append .badhash)
       --metalink-index=NUMBER     Metalink application/metalink4+xml metaurl ordinal NUMBER
       --metalink-over-http        use Metalink metadata from HTTP response headers
       --preferred-location        preferred location for Metalink resources

Directories:
  -nd, --no-directories            don't create directories
  -x,  --force-directories         force creation of directories
  -nH, --no-host-directories       don't create host directories
       --protocol-directories      use protocol name in directories
  -P,  --directory-prefix=PREFIX   save files to PREFIX/..
       --cut-dirs=NUMBER           ignore NUMBER remote directory components

HTTP options:
       --http-user=USER            set http user to USER
       --http-password=PASS        set http password to PASS
       --no-cache                  disallow server-cached data
       --default-page=NAME         change the default page name (normally
                                     this is 'index.html'.)
  -E,  --adjust-extension          save HTML/CSS documents with proper extensions
       --ignore-length             ignore 'Content-Length' header field
       --header=STRING             insert STRING among the headers
       --compression=TYPE          choose compression, one of auto, gzip and none. (default: none)
       --max-redirect              maximum redirections allowed per page
       --proxy-user=USER           set USER as proxy username
       --proxy-password=PASS       set PASS as proxy password
       --referer=URL               include 'Referer: URL' header in HTTP request
       --save-headers              save the HTTP headers to file
  -U,  --user-agent=AGENT          identify as AGENT instead of Wget/VERSION
       --no-http-keep-alive        disable HTTP keep-alive (persistent connections)
       --no-cookies                don't use cookies
       --load-cookies=FILE         load cookies from FILE before session
       --save-cookies=FILE         save cookies to FILE after session
       --keep-session-cookies      load and save session (non-permanent) cookies
       --post-data=STRING          use the POST method; send STRING as the data
       --post-file=FILE            use the POST method; send contents of FILE
       --method=HTTPMethod         use method "HTTPMethod" in the request
       --body-data=STRING          send STRING as data. --method MUST be set
       --body-file=FILE            send contents of FILE. --method MUST be set
       --content-disposition       honor the Content-Disposition header when
                                     choosing local file names (EXPERIMENTAL)
       --content-on-error          output the received content on server errors
       --auth-no-challenge         send Basic HTTP authentication information
                                     without first waiting for the server's
                                     challenge

HTTPS (SSL/TLS) options:
       --secure-protocol=PR        choose secure protocol, one of auto, SSLv2,
                                     SSLv3, TLSv1, TLSv1_1, TLSv1_2 and PFS
       --https-only                only follow secure HTTPS links
       --no-check-certificate      don't validate the server's certificate
       --certificate=FILE          client certificate file
       --certificate-type=TYPE     client certificate type, PEM or DER
       --private-key=FILE          private key file
       --private-key-type=TYPE     private key type, PEM or DER
       --ca-certificate=FILE       file with the bundle of CAs
       --ca-directory=DIR          directory where hash list of CAs is stored
       --crl-file=FILE             file with bundle of CRLs
       --pinnedpubkey=FILE/HASHES  Public key (PEM/DER) file, or any number
                                   of base64 encoded sha256 hashes preceded by
                                   'sha256//' and separated by ';', to verify
                                   peer against
       --random-file=FILE          file with random data for seeding the SSL PRNG

       --ciphers=STR           Set the priority string (GnuTLS) or cipher list string (OpenSSL) directly.
                                   Use with care. This option overrides --secure-protocol.
                                   The format and syntax of this string depend on the specific SSL/TLS engine.
HSTS options:
       --no-hsts                   disable HSTS
       --hsts-file                 path of HSTS database (will override default)

FTP options:
       --ftp-user=USER             set ftp user to USER
       --ftp-password=PASS         set ftp password to PASS
       --no-remove-listing         don't remove '.listing' files
       --no-glob                   turn off FTP file name globbing
       --no-passive-ftp            disable the "passive" transfer mode
       --preserve-permissions      preserve remote file permissions
       --retr-symlinks             when recursing, get linked-to files (not dir)

FTPS options:
       --ftps-implicit                 use implicit FTPS (default port is 990)
       --ftps-resume-ssl               resume the SSL/TLS session started in the control connection when
                                         opening a data connection
       --ftps-clear-data-connection    cipher the control channel only; all the data will be in plaintext
       --ftps-fallback-to-ftp          fall back to FTP if FTPS is not supported in the target server
WARC options:
       --warc-file=FILENAME        save request/response data to a .warc.gz file
       --warc-header=STRING        insert STRING into the warcinfo record
       --warc-max-size=NUMBER      set maximum size of WARC files to NUMBER
       --warc-cdx                  write CDX index files
       --warc-dedup=FILENAME       do not store records listed in this CDX file
       --no-warc-compression       do not compress WARC files with GZIP
       --no-warc-digests           do not calculate SHA1 digests
       --no-warc-keep-log          do not store the log file in a WARC record
       --warc-tempdir=DIRECTORY    location for temporary files created by the
                                     WARC writer

Recursive download:
  -r,  --recursive                 specify recursive download
  -l,  --level=NUMBER              maximum recursion depth (inf or 0 for infinite)
       --delete-after              delete files locally after downloading them
  -k,  --convert-links             make links in downloaded HTML or CSS point to
                                     local files
       --convert-file-only         convert the file part of the URLs only (usually known as the basename)
       --backups=N                 before writing file X, rotate up to N backup files
  -K,  --backup-converted          before converting file X, back up as X.orig
  -m,  --mirror                    shortcut for -N -r -l inf --no-remove-listing
  -p,  --page-requisites           get all images, etc. needed to display HTML page
       --strict-comments           turn on strict (SGML) handling of HTML comments

Recursive accept/reject:
  -A,  --accept=LIST               comma-separated list of accepted extensions
  -R,  --reject=LIST               comma-separated list of rejected extensions
       --accept-regex=REGEX        regex matching accepted URLs
       --reject-regex=REGEX        regex matching rejected URLs
       --regex-type=TYPE           regex type (posix|pcre)
  -D,  --domains=LIST              comma-separated list of accepted domains
       --exclude-domains=LIST      comma-separated list of rejected domains
       --follow-ftp                follow FTP links from HTML documents
       --follow-tags=LIST          comma-separated list of followed HTML tags
       --ignore-tags=LIST          comma-separated list of ignored HTML tags
  -H,  --span-hosts                go to foreign hosts when recursive
  -L,  --relative                  follow relative links only
  -I,  --include-directories=LIST  list of allowed directories
       --trust-server-names        use the name specified by the redirection
                                     URL's last component
  -X,  --exclude-directories=LIST  list of excluded directories
  -np, --no-parent                 don't ascend to the parent directory

Email bug reports, questions, discussions to <bug-wget@gnu.org>
and/or open issues at https://savannah.gnu.org/bugs/?func=additem&group=wget.
```
<a name="Tij5K"></a>
# wget命令参数详解
wget  [参数列表]  [目标软件、网页的网址] 
<a name="q4xCF"></a>
## 启动类参数
 这一类参数主要提供软件的一些基本信息:

- -V,--version    显示软件版本号然后退出；
- -h,--help      显示软件帮助信息；
- -e,--execute=COMMAND     执行一个 “.wgetrc”命令

 以上每一个功能有长短两个参数，长短功能一样，都可以使用。需要注意的是，这里的-e参数是执行一个.wgettrc的命令，.wgettrc命令其实是一个参数列表，直接将软件需要的参数写在一起就可以了。
<a name="gIOrl"></a>
## 文件处理参数
 这类参数定义软件log文件的输出方式等；

- -o,--output-file=FILE      将软件输出信息保存到文件；
- -a,--append-output=FILE    将软件输出信息追加到文件；
- -d,--debug    显示输出信息；
- -q,--quiet      不显示输出信息；
- -i,--input-file=FILE    从文件中取得URL；可以用来做批量下载。
- -nv, --non-verbose 关闭详细输出模式，但不进入安静模式。
- -F, --force-html 以 HTML 方式处理输入文件。

例1：下载 [https://www.163.com/](https://www.163.com/)   首页并且显示下载信息

```powershell
λ wget -d https://www.163.com/
```
会在当前路径下下载到网易的首页，并在控制台打印下载信息

例2：下载 [https://www.163.com/](https://www.163.com/)   首页并且不显示下载信息

```powershell
λ wget -q https://www.163.com/
```
<a name="Ubb9t"></a>
## 下载参数
 下载参数定义下载重复次数、保存文件名等；

- -t,--tries=NUMBER  是否下载次数（0表示无穷次）
-  -O --output-document=FILE  下载文件保存为别的文件名
-  -nc, --no-clobber    不要覆盖已经存在的文件,也不使用在文件名后添加 .#（# 为数字）的方法写入新的文件
-  -N,--timestamping   只下载比本地新的文件
-  -T,--timeout=SECONDS   设置超时时间
-  -Y,--proxy=on/off  关闭代理
- –-limit-rate  下载限速
- -c, --continue 断点续传
- -b 后台下载
- --spider 测试下载链接，可用于定时下载、检查网站是否有死链接等场合。

例：使用wget -O下载并以不同的文件名保存

```powershell
λ wget -O test.html https://www.163.com/
--2019-05-23 17:52:57--  https://www.163.com/
Resolving www.163.com (www.163.com)... 101.246.182.209, 220.112.197.91
Connecting to www.163.com (www.163.com)|101.246.182.209|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: 'test.html'

test.html                                                [  <=>                                                                                                                 ] 685.06K  2.34MB/s    in 0.3s

2019-05-23 17:52:57 (2.34 MB/s) - 'test.html' saved [701504]
```
使用 `--spider`  判断url有效的例子

```powershell
λ wget --spider https://www.163.com
Spider mode enabled. Check if remote file exists.
--2019-05-23 19:57:54--  https://www.163.com/
Resolving www.163.com (www.163.com)... 101.246.182.209
Connecting to www.163.com (www.163.com)|101.246.182.209|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Remote file exists and could contain further links,
but recursion is disabled -- not retrieving.
```
 使用 `--spider`  判断url无效的例子

```powershell
λ wget --spider 192.168.1.203
Spider mode enabled. Check if remote file exists.
--2019-05-23 19:59:33--  http://192.168.1.203/
Connecting to 192.168.1.203:80... failed: Unknown error.
Retrying.
```

<a name="h14AY"></a>
## 目录参数
目录参数主要设置下载文件保存目录与原来文件（服务器文件）的目录对应关系；

- 　-nd --no-directories 不建立目录
-    -x,--force-directories 强制建立目录
-    -P, --directory-prefix=名称 保存文件前先创建指定名称的目录。
-    --cut-dirs=数目 忽略远程目录中指定数目的目录层。


例：下载[https://www.163.com/](https://www.163.com/) 的首页，并且保持网站结构

```powershell
λ wget -x  https://www.163.com/
--2019-05-23 17:57:09--  https://www.163.com/
Resolving www.163.com (www.163.com)... 101.246.182.209, 220.112.197.91
Connecting to www.163.com (www.163.com)|101.246.182.209|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: 'www.163.com/index.html'

www.163.com/index.html                                   [ <=>                                                                                                                  ] 685.17K  3.48MB/s    in 0.2s

2019-05-23 17:57:10 (3.48 MB/s) - 'www.163.com/index.html' saved [701609]
```
在没有使用 `-x` 参数时，下载的文件直接会保存为当前目录下的 `index.html` ,加上上面的参数后，会在当前目录下多建立一个 `www.163.com` 的文件夹， `index.html` 就会放在改目录下面。
<a name="znqR7"></a>
## http参数
HTTP参数设置一些与HTTP下载有关的属性；

-  --http-user=USER   设置HTTP用户
-  --http-passwd=PASS   设置HTTP密码
-  --proxy-user=USER   设置代理用户
-  --proxy-passwd=PASS   设置代理密码
- -C, --cache=on/off (不)使用服务器中的高速缓存中的数据 (默认是使用的
- --cookies=off 禁用 cookie。
- --load-cookies=文件 会话开始前由指定文件载入 cookie。
- --save-cookies=文件 会话结束后将 cookie 保存至指定文件。
- --post-data=字符串 使用 POST 方法，发送指定字符串。
- --post-file=文件 使用 POST 方法，发送指定文件中的内容。
<a name="ovdo8"></a>
## HTTPS (SSL) 选项

- --sslcertfile=文件 可选的客户段端证书。
- --sslcertkey=密钥文件 对此证书可选的“密钥文件”。
- --egd-file=文件 EGD socket 文件名。
- --sslcadir=目录 CA 散列表所在的目录。
- --sslcafile=文件 包含 CA 的文件。
- --sslcerttype=0/1 Client-Cert 类型 0=PEM (默认) / 1=ASN1 (DER)
- --sslcheckcert=0/1 根据提供的 CA 检查服务器的证书
- --sslprotocol=0-3 选择 SSL 协议；0=自动选择，1=SSLv2 2=SSLv3 3=TLSv1
<a name="T6mx7"></a>
## FTP 选项

- -nr, --dont-remove-listing 不删除“.listing”文件。
- -g, --glob=on/off 设置是否展开有通配符的文件名。
- --passive-ftp 使用“被动”传输模式。
- --retr-symlinks 在递归模式中，下载链接所指示的文件(连至目录则例外）

<a name="T9c7j"></a>
## 递归参数设置
在下载一个网站或者网站的一个目录的时候，我们需要知道的下载的层次，这些参数就可以设置；

- 　　-r,--recursive 下载整个网站、目录（小心使用）
- 　　-l,--level=NUMBER 下载层次
- --delete-after 删除下载后的文件。
- -k, --convert-links 将绝对链接转换为相对链接。
- -K, --backup-converted 转换文件 X 前先将其备份为 X.orig。
- -m, --mirror 等效于 -r -N -l inf -nr 的选项。
- -p, --page-requisites 下载所有显示完整网页所需的文件，例如图像。
- --strict-comments 打开对 HTML 备注的严格(SGML)处理选项。


```powershell
λ wget -rx  https://www.163.com/
```
<a name="5GGq8"></a>
## 递归允许与拒绝选项参数
<br />下载一个网站的时候，为了尽量快，有些文件可以选择下载，比如图片和声音，在这里可以设置:

- -A,--accept=LIST    可以接受的文件类型列表，以逗号分隔
-  -R,--reject=LIST    拒绝接受的文件类型列表，以逗号分隔，例如 --reject=gif 
-  -D,--domains=LIST   可以接受的域名列表，以逗号分隔
-  --exclude-domains=LIST   拒绝的域名列表，以逗号分隔
-  -L,--relative   下载关联链接
-  --follow-ftp   只下载FTP链接
-  -H,--span-hosts    可以下载外面的主机
-  -I,--include-directories=LIST   允许的目录
-  -X,--exclude-directories=LIST    拒绝的目录

<a name="WLnjW"></a>
# 福利时间
一个综合案例，下载网站图片，以知乎网站的一个问题为例：[大胸女生如何穿衣搭配](https://www.zhihu.com/question/26297181/answer/633004295)

打开控制台执行这个 ` copy($$('img').map(function(item){return item.src}).join("\r\n"))` 
> copy() 可以将在控制台获取到的内容复制到剪贴板
> $$ 符号来选择所有匹配规则的DOM元素。选择返回的结果是一个数组，可以通过数组的方法来访问其中的单个元素。 
> 这些都是chrome的方法，具体可以参见另一篇文章：https://www.yuque.com/docs/share/c6486d4d-5f83-4919-817b-f0c6163f8b09   


`$$('img').map(function(item){return item.src}).join("\r\n")` 的效果如下:<br />![实战.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558625825196-cd2f22b6-1e73-4140-9280-9329e670caad.png#align=left&display=inline&height=433&name=%E5%AE%9E%E6%88%98.png&originHeight=433&originWidth=1236&size=91542&status=done&width=1236)

然后把copy的地址放在一个文件`url.txt`内

```
https://pic3.zhimg.com/80/v2-4e352b045ef4e89b09061fbf6fbe2184_hd.jpg
https://pic2.zhimg.com/80/v2-572a2df584f115b7511fef7d8074124b_hd.jpg
https://pic1.zhimg.com/80/v2-a508c534c91f32592a40ab72788b9570_hd.jpg
https://pic3.zhimg.com/80/v2-a4422ec6d54bba486b05f6bf6c4dcde1_hd.jpg
https://pic4.zhimg.com/80/v2-3e20349156aa88764604bc9a94580efc_hd.jpg
https://pic2.zhimg.com/80/v2-f990d8f86210c2546c62fedad672fc08_hd.jpg
https://pic4.zhimg.com/80/v2-728c3884413b0fbe77a7520a82570344_hd.jpg
https://pic1.zhimg.com/80/v2-e74456986d46be5bd10a80b4bbce14b9_hd.jpg
https://pic3.zhimg.com/80/v2-49d5cc3a363775896cb3b2d6daa21975_hd.jpg
https://pic1.zhimg.com/80/v2-6f9393a74e9b649eb1888d40533e33f9_hd.jpg
https://pic3.zhimg.com/80/v2-0e733c25629977a6d13aecf744c126cc_hd.jpg
https://pic2.zhimg.com/80/v2-cfe3511c518d679725314a796d958a31_hd.jpg
https://pic2.zhimg.com/80/v2-bf9d53adc05e5d3c1315b90799d416fb_hd.jpg
https://pic1.zhimg.com/80/v2-850ece0e547f106daaad1f7441b0d9b3_hd.jpg
https://pic4.zhimg.com/80/v2-2d76f3806e357913bb23b2d4cd5509a8_hd.jpg
https://pic3.zhimg.com/80/v2-816b5f16fec94db8e26eccbf40080225_hd.jpg
https://pic1.zhimg.com/80/v2-85301218fd7df0d9823e2714e5b1f517_hd.jpg
https://pic1.zhimg.com/v2-49c9c9345d8ad3bf37bba9447a5e143e_xs.jpg
https://pic1.zhimg.com/aadd7b895_xs.jpg
https://pic3.zhimg.com/90/v2-d9e93a3b23f6fe8ff5bfbb07317dce9f_250x0.jpg
https://pic3.zhimg.com/90/eaf9b0b881669929994d4802ee14de28_250x0.jpg
https://pic1.zhimg.com/90/v2-ac20b8c06a43597b6fade38048a480e4_250x0.jpg
```
接下来用[wget](https://links.jianshu.com/go?to=http%3A%2F%2Fgnuwin32.sourceforge.net%2Fpackages%2Fwget.htm)一键下载。`wget -i url.txt -P ./zhihu` 所有图片都下载到本地目录zhihu了。

