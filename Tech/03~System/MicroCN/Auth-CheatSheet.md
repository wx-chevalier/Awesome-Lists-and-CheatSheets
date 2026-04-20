# Auth CheatSheet | 权限认证机制概述

可以阅读 [Web 安全实践清单](https://parg.co/GWc) 了解权限校验、密码规范等安全相关知识。WebAPI 或者 RPC 接口，[HTTP CheatSheet]()，[DOM CheatSheet/数据存储]()。

![Session, cookie, JWT, token, SSO, and OAuth 2.0](https://pic.imgdb.cn/item/63885ca816f2c2beb1ff12ce.jpg)

- WWW-Authenticate 是最基本的方法，浏览器会要求你提供用户名和密码。由于无法控制登录的生命周期，现在已经很少使用了。
- 对登录生命周期的更精细的控制是 session-cookie。服务器保持会话存储，而浏览器则保持会话的 ID，一个 cookie 通常只适用于浏览器，对移动应用不友好。
- 使用 token 来解决兼容性问题，客户端将令牌发送给服务器，而服务器则验证令牌的有效性。缺点是需要对令牌进行加密和解密，这可能很耗时。
- JWT 是一种代表令牌的标准方式。这种信息可以被验证和信任，因为它是数字签名的。由于 JWT 包含签名，所以不需要在服务器端保存会话信息。
- 通过使用 SSO（单点登录），你可以只登录一次，并登录到多个网站。它使用 CAS（中央认证服务）来维护跨网站信息
- 通过使用 OAuth 2.0，你可以授权一个网站访问你在另一个网站的信息

# HTTP Basic 认证

桌面应用程序也通过 HTTP 协议跟 Web 服务器交互，桌面应用程序一般不会使用 cookie, 而是把 " 用户名 + 冒号 + 密码 " 用 BASE64 算法加密后的字符串放在 http request 中的 header Authorization 中发送给服务端，这种方式叫 HTTP 基本认证 (Basic Authentication)

当浏览器访问使用基本认证的网站的时候，浏览器会提示你输入用户名和密码，如下图

![](http://pic002.cnblogs.com/images/2012/263119/2012092510283354.png)

假如用户名密码错误的话，服务器会返回 401 如下图

![](http://pic002.cnblogs.com/images/2012/263119/2012092510293780.png)

HTTP 基本认证的过程

第一步 : 客户端发送 http request 给服务器，

第二步 : 因为 request 中没有包含 Authorization header, 服务器会返回一个 401 Unauthozied 给客户端，并且在 Response 的 header "WWW-Authenticate" 中添加信息。

![](http://pic002.cnblogs.com/images/2012/263119/2012092121494456.png)

第三步：客户端把用户名和密码用 BASE64 加密后，放在 Authorization header 中发送给服务器，认证成功。

第四步：服务器将 Authorization header 中的用户名密码取出，进行验证，如果验证通过，将根据请求，发送资源给客户端

![](http://pic002.cnblogs.com/images/2012/263119/2012092121495881.png)

使用 Fiddler Inspectors 下的 Auth 选项卡，可以很方便的看到用户名和密码

![](http://pic002.cnblogs.com/images/2012/263119/2012092121505442.png)

HTTP 基本认证的优点

HTTP 基本认证，简单明了。Rest API 就是经常使用基本认证的。

每次都要进行认证

http 协议是无状态的，同一个客户端对 服务器的每个请求都要求认证。

# 基于 Session 的认证

Cookie 与 Session 的存在主要是为了解决 HTTP 这一无状态协议下服务器如何识别用户的问题，其原理就是在用户登录通过验证后，服务端将数据加密后保存到客户端浏览器的 Cookie 中，同时服务器保留相对应的 Session（文件或 DB）。用户之后发起的请求都会携带 Cookie 信息，服务端需要根据 Cookie 寻回对应的 Session，从而完成验证，确认这是之前登陆过的用户。其工作原理如下图所示：

![image](https://user-images.githubusercontent.com/5803001/43043318-d9211e10-8dc3-11e8-806c-e3074eb4dd39.png)

# 基于 Token 的认证

## JSON Web Token

# OAuth

# 认证策略

## 单点登录

## 2FA 双因子认证
