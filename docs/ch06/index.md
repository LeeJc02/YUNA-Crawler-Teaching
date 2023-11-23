# 来玩点高端的O(∩_∩)O

## 1. 反爬机制

-   **反爬机制**: 你要爬取, 我不让你爬, 设置了关卡检测你是不是个人 ( 验证码, 速度, cookie, 代理信息 )

-   在之前我们介绍了**请求头**里的User-Agent (用户代理) 是包含了客户端的相关信息，通常包括浏览器类型、版本和操作系统等

-   客户端在响应之前需要检查请求头的东西是否合法进行匹配
    -   **检测请求头正常**: 正常响应发送响应头并建立连接
    -   **检测异常**: 无法建立连接, 打开页面失败
-   User-Agent包含了请求的载体身份标识, 常用来作为服务器检测的标志

## 2. UA检测

-   **UA检测**: 服务器对你发送的请求头进行分析:
    -   身份信息为某一浏览器 ---> 正常用户请求 ---> 允许获取数据
    -   身份信息缺失或异常 ---> 异常访问请求 ---> 拒绝获取数据
-   **省流**: 对你发送的请求里面的身份信息进行验证

## 3. 反反爬策略

-   **反反爬策略**: 你不让我爬, 我想个办法就要爬
-   通常反反爬可以通过**绕过, 第三方解决, 伪装, 降速**等方法去解决相应的反爬机制
-   上有政策下有对策, 爬虫通过python广泛的第三方库能够有各种各样的解决方法, 通常也能实现破解等功能

## 4. UA伪装

-   既然服务器要检测User-Agent, 那我们**伪装成浏览器身份信息**就绕过了UA检测

-   我们同样通过上次写的函数实现, get函数原型如下

```py
def get(
    url: str | bytes,
    params: _Params | None = None,
    *,
    data: _Data | None = ...,
    headers: _HeadersMapping | None = ...,
    cookies: RequestsCookieJar | _TextMapping | None = ...,
    files: _Files | None = ...,
    auth: _Auth | None = ...,
    timeout: _Timeout | None = ...,
    allow_redirects: bool = ...,
    proxies: _TextMapping | None = ...,
    hooks: _HooksInput | None = ...,
    stream: bool | None = ...,
    verify: _Verify | None = ...,
    cert: _Cert | None = ...,
    json: Incomplete | None = ...,
) -> Response: ...
```

-   通过之前python的学习, 我们可以看出除了必要的url参数之外, 该函数还有个很多默认的参数, 包含了各种**请求头信息**的所有信息, 我们可以传入需要的参数以达到伪装自己的效果
-   为了UA伪装, 我们需要封装User-Agent作为爬虫程序的请求头

```py
header = { 'User-Agent':'________'} # 填浏览器复制的User-Agent信息
response = requests.get(url=url,headers=head)
```

-   以字典封装一个键为`User-Agent`的字典作为headers参数传入实现伪装



## 这样你就绕过了服务器的UA检测！！

## 恭喜你完成了第一步的反反爬！！

