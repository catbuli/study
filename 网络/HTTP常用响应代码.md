# HTTP常用响应代码

## 1XX - Informational（信息性状态码）

## 2XX - Success（成功状态码）

**`200 OK` - 请求正常处理**

**`204 No Content` - 请求处理成功，但没有任何资源可以返回**

> 可以用来当作返回信息，省掉多余的数据传输。

## 3XX - Redirection（重定向状态码）

**`301 Moved Permanently` - 永久性重定向**

> 主要是将需要转移的网址重定向另一个新的网址上，并且是永久性转移。

**`302 Found` - 临时性重定向**

> 重定向的目标还有可能发生改变。

**`303 See Other` - 303重定向**

> 它表示重定向链接指向的不是新上传的资源，而是另外一个页面，比如消息确认页面或上传进度页面。
> 这部分我的理解比较模糊。

**`304 Not Modified` - 未改变**

> 说明无需再次传输请求的内容，也就是说可以使用缓存的内容。

## 4XX - Client Error（客户端错误状态码）

**`400 Bad Request` - 坏请求**

> 服务端无法理解客户端的请求，可能是请求中存在语法错误。

**`401 Unauthorized` - 缺乏身份验证信息**

> 这个状态码会与  [`WWW-Authenticate`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/WWW-Authenticate) 首部一起发送，其中包含有如何进行验证的信息。

**`403 Forbidden` - 不允许访问**

> 服务器端有能力处理该请求，但是拒绝授权访问。

**`404 Not Found` - 未找到**

> 客户端错误，指的是服务器端无法找到所请求的资源。

**`405 Method Not Allowed` - 方法不被允许**

> 表明服务器禁止了使用当前 HTTP 方法的请求。

## 5XX - Server Error（服务器错误状态码）

**`500 Internal Server Error` - 服务器错误**

> 表示服务器端错误的响应状态码，意味着所请求的服务器遇到意外的情况并阻止其执行请求。

**`503 Service Unavailable` - 服务器不可用**

> 表示服务器尚未处于可以接受请求的状态。通常出现在服务器超载，或因为维护停机的情况。

# 资料来源

[HTTP 响应代码 - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)