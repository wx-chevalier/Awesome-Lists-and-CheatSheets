# Web 安全实践清单

[OWASP 2017](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf)

[![websecurity](https://user-images.githubusercontent.com/5803001/36406391-4fae0aee-1631-11e8-9f07-1bfe67f1cfc4.png)](https://www.processon.com/view/link/5a8b94d5e4b0615ac05a5698)

# 校验过滤

数值处理：

- 不正确的数组索引验证/CWE 129: 直接使用外部输入或计算值作为数组索引；编码错误导致的数组索引差一；外部输入作为循环阈值，导致越界访问。

- 数值类型间的不正确转换/CWE 681: 大类型数向小类型数转换时发生截断；小类型有符号数跨级别转化为大类型无符号数时，中间发生的隐式转换导致数值错误；不同类型参与表达式发生隐式转换，导致计算结果非预期；有符号类型和无符号类型相互转换发生符号错误，参与表达式计算结果非预期。

- 整数溢出或回绕/CWE 190: 数值变量加减乘运算溢出；数值变量自加、自减运算溢出；指针变量偏移运算溢出。

- 缓冲区大小计算不正确/CWE 131: 申请内存的大小比实际使用的内存小；申请内存大小的计算表达式计算值比实际使用的内存小。

# SQL 注入

- 执行外部拼接的 SQL 语句。

- 执行外部传入的整条 SQL 语句。

- 在配置文件中的 SQL 语句没有使用预编译方式占位符。

- 校验函数有缺陷或者占位符使用错误。

# XSS

- 通过 HTTP 请求对输入参数注入脚本，利用 HTML 协议多样性，使用不同编码方式构造复杂的脚本，绕过防火墙、参数校验，在页面展现、执行输入数据。

- 对数据来源于数据库、文件系统等不可信数据源，直接在页面展现、执行输入数据。

- 富文本控件中内容校验可能被绕开，导致恶意脚本执行。

# 命令注入

- 应用主动调用系统命令或者 Shell 脚本完成特定功能时导致的命令注入。

- 通过语言解释器(OGNL)或者 eval 函数注入代码，调用对应语言的系统调用函数调用系统命令。

- 通过 SQL 注入调用数据库的系统存储过程，如 xp_cmdshell 等完成命令调用。

# CSRF

CSRF (Cross Site Request Forgery，跨站点请求伪造)是一种常见的网络攻击方式，也是在公网提供 HTTP 接口绕不开的一个坎，需要前后端一起配合才能做好 CSRF 防护。

假设有一个银行站点，提供一个 HTTP 接口允许当前登录的用户将其账户中的钱转移到另外一个账户中。该 HTTP 接口定义为：

```yaml
POST /transfer HTTP/1.1
Host: bank.example.com
Cookie: JSESSIONID=randomid; Domain=bank.example.com; Secure; HttpOnly
Content-Type: application/x-www-form-urlencoded
```

amount=100.00&routingNumber=1234&account=9876
我们登录该银行网站以后，访问另外一个恶意网站页面，该页面包含如下代码片段：

```html
<form action="https://bank.example.com/transfer" method="post">
  <input type="hidden" name="amount" value="100.00" />
  <input type="hidden" name="routingNumber" value="evilsRoutingNumber" />
  <input type="hidden" name="account" value="evilsAccountNumber" />
  <input type="submit" value="Win Money!" />
</form>
```

如果我们点击上述表单中的提交按钮后，不知不觉中，我们账户中的钱会被转走。这就是一个简单的 CSRF 攻击。CSRF 漏洞攻击的过程中，用户可能没有任何感知，因为可以使用 Javascript 自动完成。CSRF 的攻击请求可以和真实的请求一模一样，服务端无法识别请求的“合法性”。因为请求的所有参数都是已知的，容易被伪造。

为了防范 CSRF 攻击，我们需要保证请求中包含某个信息，该信息是伪造的请求无法提供的，服务端可以判断请求的合法性。可能的防范手段包括：

- 验证码：要求用户的人工干预，安全有效，但是用户体验很差。

- HTTP Referer：只信赖可信的 Referer 源。但是，服务端并非总能收到 Referer。例如 1）https 跳转 http 时浏览器可能不发送 Referer；2）某些客户端允许用户自定义 Referer 头域等。

- CSRF Token：针对 CSRF 问题，目前通行的做法客户端请求中携带一个 Token，服务端收到请求后校验请求中 Token 的合法性。需要注意的是，该 Token 随机生成、不可预测，且被客户端和服务端所共享。Token 一般由服务端生成后保存，客户端可以以某种安全的方式获取到 Token。

客户端向服务端发送请求时携带 CSRF Token 的方式有两种：

- HTTP 请求头：默认的请求头名称为 X-CSRF-TOKEN，也可以自定义后做配置生效

```yaml
POST /csrf-required-path HTTP/1.1
Host: www.example.com
Cookie: xxxx
X-XSRF-TOKEN: 8fba1604-8c0d-4619-973c-ac1a79b90298
```

- HTTP 请求参数：默认的参数名为\_csrf，也可自定义后做配置生效

```yaml
POST /csrf-required-path HTTP/1.1
Host: www.example.com
Cookie: xxxx

param1=value1&_csrf=8fba1604-8c0d-4619-973c-ac1a79b90298
```

# Links

- https://blog.logrocket.com/security-for-fullstack-web-developers-part-1-a56340283f7c

- https://juejin.im/post/5c446eb1e51d45517624f7db
