# 除了HTML我们还能爬什么?

## 1. 异步通信大师 ---- 阿贾克斯(AJAX)

-   很多时候web界面都只是加载了一部分界面, 等我们往下翻或者点击什么才会跳出来, 而原页面并不会跳转, 而是在原界面进行加载别的东西
-   **异步通信**: 消息发送方和接收方的操作不需要同时发生。在异步通信中，发送方将消息发送给接收方，然后继续执行其它任务，而不必等待接收方立即响应

-   **省略**: 给你一碗饭你先吃着, 你还要吃我再重新给你煮
-   在Web开发中，异步通信允许通过AJAX（Asynchronous JavaScript and XML）向服务器发送HTTP请求，同时允许用户在等待响应时继续与页面交互

## 2. 抓捕阿贾克斯行动

-   AJAX是在原界面的添加行为, 所以爬取应该用post类型进行访问

```py
def post(
    url: str | bytes,
    data: _Data | None = None,
    json: Incomplete | None = None,
    *,
    params: _Params | None = ...,
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
) -> Response: ...
```

-   通过检测工具可以找到我们所需要的AJAX的数据包, **Request Method为post类型**, **Content-Type为json类型** (JavaScript Object Notation), 即响应数据为json型
-   对于json文件我们有专门的内置函数库, 以调用对json进行操作的函数
-   在获取json类型后我们需要将其**响应对象**转换为**json对象**并用特殊的`json.dump`函数进行写入文件

```py
import json
...
json_text = response.json()
with open('./dog.json','w',encoding='utf-8')as fp:
	json.dump(responce.json(),fp=fp,ensure_ascii=False)
# json.dump(obj，fp，*，ensure_ascii)
```

-   `json.dump`函数默认以`ASCII`编码进行编码和解码, 若json文件中含有中文需要False以使用`UTF-8`编码

## 你爬到了一个AJAX异步通信实现的JSON文件！！