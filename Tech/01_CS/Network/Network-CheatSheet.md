# HTTP CheatSheet | HTTP 相关必知必会：TCP/HTTP2/HTTPS/DNS，请求，响应，缓存

HTTP, 等网络协议是我们日常开发、面试中常见的知识要点。

```sh
http://rob:abcd1234@www.example.co.uk/path/index.html?query1=test&silly=willy&field[0]=zero&field[2]=two#test=hash&chucky=cheese
```

# 基础

## URI & URL

The difference between them is straightforward after knowing their definitions:

- **Uniform Resource Identifier (URI)** − a sequence of characters that allows the complete identification of any abstract or physical resource
- **Uniform Resource Locator (URL)** − a subset of URI that, in addition to identifying where a resource is available, describes the primary mechanism to access it

Every URI, regardless if it’s a URL or not, follows a particular form:

```
scheme:[//authority][/path][?query][#fragment]
```

Where each part is described as follows:

- **\*scheme\*** − for URLs, is the name of the protocol used to access the resource, for other URIs, is a name that refers to a specification for assigning identifiers within that scheme
- **authority** − an optional part comprised of user authentication information, a host and an optional port
- **\*path\*** − it serves to identify a resource within the scope of its _scheme_ and _authority_
- **\*query\*** − additional data that, along with the _path,_ serves to identify a resource. For URLs, this is the query string
- **\*fragment\*** − an optional identifier to a specific part of the resource

**To easily identify if a particular URI is also a URL, we can check its scheme**. Every URL has to start with any of these schemes: _ftp_, _http_, _https,_ _gopher_, _mailto_, _news_, _nntp_, _telnet_, _wais_, _file_, or _prospero_. If it doesn’t start with it, then it’s not a URL.

# 请求

# 响应

## 常用响应头

- Content-Disposition

Content-Disposition 属性是作为对下载文件的一个标识字段，属性有两种类型: inline 将文件内容直接显示在页面, attachment 弹出对话框让用户下载:

```
Content-Type: image/jpeg
Content-Disposition: inline;filename=hello.jpg
Content-Description: just a small picture of me
```

# 缓存

# TCP

![image](https://user-images.githubusercontent.com/5803001/48391511-ea06ba00-e741-11e8-832f-ac9d994f0b21.png)

这是因为 Linux 不像其他操作系统在收到 SYN 为该连接立马分配一块内存空间用于存储相关的数据和结构，而是延迟到接收到 client 的 ACK，即三次握手 真正完成后才分配空间，这是为了防范 SYN flooding 攻击。如果是这种情况，那么就会出现 client 端未 ESTABLISHED 状态，server 为 SYN_RECV 状态。

| CLOSED       | 没有使用这个套接字[netstat 无法显示 closed 状态]                                                                                          |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| LISTEN       | 套接字正在监听连接[调用 listen 后]                                                                                                        |
| SYN_SENT     | 套接字正在试图主动建立连接[发送 SYN 后还没有收到 ACK]                                                                                     |
| SYN_RECEIVED | 正在处于连接的初始同步状态[收到对方的 SYN，但还没收到自己发过去的 SYN 的 ACK]                                                             |
| ESTABLISHED  | 连接已建立                                                                                                                                |
| CLOSE_WAIT   | 远程套接字已经关闭：正在等待关闭这个套接字[被动关闭的一方收到 FIN]                                                                        |
| FIN_WAIT_1   | 套接字已关闭，正在关闭连接[发送 FIN，没有收到 ACK 也没有收到 FIN]                                                                         |
| CLOSING      | 套接字已关闭，远程套接字正在关闭，暂时挂起关闭确认[在 FIN_WAIT_1 状态下收到被动方的 FIN]                                                  |
| LAST_ACK     | 远程套接字已关闭，正在等待本地套接字的关闭确认[被动方在 CLOSE_WAIT 状态下发送 FIN]                                                        |
| FIN_WAIT_2   | 套接字已关闭，正在等待远程套接字关闭[在 FIN_WAIT_1 状态下收到发过去 FIN 对应的 ACK]                                                       |
| TIME_WAIT    | 这个套接字已经关闭，正在等待远程套接字的关闭传送[FIN、ACK、FIN、ACK 都完毕，这是主动方的最后一个状态，在过了 2MSL 时间后变为 CLOSED 状态] |

TCP 协议规定，对于已经建立的连接，网络双方要进行四次握手才能成功断开连接，如果缺少了其中某个步骤，将会使连接处于假死状态，连接本身占用的资源不会被释放。网络服务器程序要同时管理大量连接，所以很有必要保证无用连接完全断开，否则大量僵死的连接会浪费许多服务器资源。在众多 TCP 状态中，最值得注意的状态有两个：CLOSE_WAIT 和 TIME_WAIT。

CLOSE_WAIT 对方主动关闭连接或者网络异常导致连接中断，这时我方的状态会变成 CLOSE_WAIT 此时我方要调用 close()来使得连接正确关闭；TIME_WAIT 是我方主动调用 close()断开连接，收到对方确认后状态变为 TIME_WAIT。TCP 协议规定 TIME_WAIT 状态会一直持续 2MSL(即两倍的分段最大生存期)，以此来确保旧的连接状态不会对新连接产生影响。处于 TIME_WAIT 状态的连接占用的资源不会被内核释放，所以作为服务器，在可能的情况下，尽量不要主动断开连接，以减少 TIME_WAIT 状态造成的资源浪费。

# HTTPS

HTTPS 要使客户端与服务器端的通信过程得到安全保证，必须使用的对称加密算法，但是协商对称加密算法的过程，需要使用非对称加密算法来保证安全，然而直接使用非对称加密的过程本身也不安全，会有中间人篡改公钥的可能性，所以客户端与服务器不直接使用公钥，而是使用数字证书签发机构颁发的证书来保证非对称加密过程本身的安全。这样通过这些机制协商出一个对称加密算法，就此双方使用该算法进行加密解密。从而解决了客户端与服务器端之间的通信安全问题。

![image](https://pic.imgdb.cn/item/611143f05132923bf8cd4086.png)

![image](https://pic.imgdb.cn/item/6111440f5132923bf8cda2a9.png)

# HTTP/2

# WebSocket

# DNS

Dns 系统主要是依靠权威 dns，和递归 dns 来工作的。权威 dns 做的事情主要是管理某个或多个特定域的 dns 服务。一般大一点的公司，都有自己的权威 dns

比如所有”.alipay.com”结尾的域名都由 alipay 来管理

所有”.alibaba.com”结尾的域名都由 alibaba 来管理(alipay 和 alibaba 实际又是同一家公司来管理)

所有“.baidu.com”结尾的域名都由 baidu 来管理

Alibaba 和 baidu 各管各的，没有交互。一级域要去根上注册，像 com 域，net 域就属于一级域

Com 域（也就是所有以“.com”结尾的老祖 com 域）要去根上注册 com 域的域名服务器（nameserver）列表。

Net 域（也就是所有以”.net”结尾的老祖 net 域）要去根上注册 net 域的域名服务器（nameserver）列表。二级域一般要到一级域上去注册

alibaba.com 要到 com 域去注册自己的域名服务器 nameserver 列表

Baidu.com 也要到 com 域去注册自己的域名服务器 nameserver 列表

![i20180520_181112_186](https://user-images.githubusercontent.com/5803001/40573917-a5b3da1c-60fb-11e8-8be9-7ad479c05daa.jpg)

递归 DNS（Recursion DNS）

那用户访问 www.alibaba.com，请求又是如何到 alibaba 的权威 dns 服务器上面找到 www.alibaba.com 的 ip 呢？

这个时候递归 dns（我们一般叫做 local dns）就介入了。递归 dns 也就是我们常说的缓存 dns，local dns，公共 dns（提供专门递归服务的 dns），这样一步步的从根“.”到"com",再到“alibaba.com”,最后到“www.alibaba.com”的过程叫做递归过程
Dns 请求一般是 udp 报文（也可以是 tcp 的报文），所以同样也是要有源 ip，目标 ip，等等这些网络数据包的底层信息，递归过程的每一步，目标 ip 都必须是很明确的
各个域的 namserver 实际上是有多台的，比如根的 namserver 的 ip 有 13 个，com 的 namserver 的 ip 也有 13 个，递归 dns 在进行递归时需要选择其中一个 ip 作为目标 ip 进行下一步请求即可（目前主流 dns 实现软件，如 bind 会选择延时最小的那个 ip 作为下一步请求的目标 ip）dns 中用的多的是 anycast 技术，一个 ip 实际上对了很多个物理服务器，到各个权威 nameserver 上，也有 lvs，ospf 等等一些负载均衡技术把同一个 ip 对应到多个物理服务器上面。
递归 dns 还会把图中递归第一步，第二步，第三步向各级权威 dns 发起的请求结果给缓存到自己的内存中，直到这条结果的 ttl 超期失效（超期时间一般为几分钟到几小时几天等等），在这个 ttl 超期之前，任何其他用户发起的 www.alibaba.com 的 dns 请求，递归 dns 都会直接从自己的内存中把缓存结果直接返回给客户端（不会去递归了）。如果 ttl 超期了，才会去重新递归。

有的 dns 既是权威 dns，又是递归 dns，这并不冲突，这种 dns 在遇到域名是自己管理的域的后缀结尾时，会直接进行应答（无论是否存在结果），如果不是自己管理的域的后缀域名，则进行递归，同样吧递归结果进行缓存。
