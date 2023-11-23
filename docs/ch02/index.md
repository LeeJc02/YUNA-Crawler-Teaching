# 超超超超简单的爬虫小原理! ! !

## 1. 爬虫是个啥?

-   爬虫: 是一种自动化程序或脚本，用于在互联网上浏览和收集网页数据。爬虫的主要目的是从网站或Web服务器上获取信息、数据或内容，并将其保存到本地存储或用于其他用途

-   **省流**: 爬虫就是**编写程序**, 让程序**模拟用户登录**访问数据, 把**数据爬取**进行存储或计算

## 2. 论一只爬虫的工作原理

1.   一只有智慧的爬虫进化出了人的思想!
2.   小爬虫打开了浏览器并输入了URL
3.   小爬虫等待HTTP请求之后建立连接
4.   小爬虫打开了这个网页并看到了数据! ! !
5.   小爬虫把所有的网页数据打包带回了家

## 3. 程序实践

-   python: 虽然爬得慢, 但是**写的快**啊

-   通过python的requests模块 (相当于C语言中的一个头文件, 里面包含了一个方面的很多函数) 进行编写可以自动访问服务器并进行数据分析拿到想要的数据，我们通过pip命令下载．

    ```py
    pip install requests
    ```

-   爬取的数据进行数据处理保存让你能够看到

-   下面是一个优美的简单小爬虫

```python
import requests
response = requests.get('https://bilibili.com').text
print(response)
```

-   如此你将会获得以下打印数据

```html
<!DOCTYPE html>
<html>
<head><title>验证码_哔哩哔哩</title>
    <meta name="viewport"
          content="width=device-width,user-scalable=no,initial-scale=1,maximum-scale=1,minimum-scale=1,viewport-fit=cover">
    <meta name="spm_prefix" content="333.1291">
    <script type="text/javascript"
            src="//www.bilibili.com/gentleman/polyfill.js?features=Promise%2CObject.assign%2CString.prototype.includes%2CNumber.isNaN"></script>
    <script>
        window._riskdata_ = {
            'v_voucher': 'voucher_d205b9b3-8844-4cd1-a71d-b6b553ae2360'
        }
    </script>
    <script type="text/javascript" src="//s1.hdslb.com/bfs/seed/log/report/log-reporter.js"></script>
    <link href="//s1.hdslb.com/bfs/static/jinkela/risk-captcha/css/risk-captcha.0.da69749d1b28e8499cd7d913726fa7af74949406.css"
          rel="stylesheet">
</head>
<body>
<div id="biliMainHeader"></div>
<div id="risk-captcha-app"></div>
<script src="//s1.hdslb.com/bfs/seed/jinkela/risk-captcha-sdk/CaptchaLoader.js"></script>
<script type="text/javascript"
        src="//s1.hdslb.com/bfs/static/jinkela/risk-captcha/1.risk-captcha.da69749d1b28e8499cd7d913726fa7af74949406.js"></script>
<script type="text/javascript"
        src="//s1.hdslb.com/bfs/static/jinkela/risk-captcha/risk-captcha.da69749d1b28e8499cd7d913726fa7af74949406.js"></script>
</body>
</html>

```

## 4. 爬虫的分类 (供大家了解)

1.  **按用途分类**：
    -   **通用爬虫**：通用爬虫旨在收集互联网上的所有信息，以建立搜索引擎的索引。它们通过遍历整个互联网来发现和收集网页。
    -   **聚焦爬虫**：聚焦爬虫专注于特定领域或主题，例如新闻、社交媒体、电子商务网站等，以获取相关信息。
    -   **深层爬虫**：深层爬虫用于获取动态生成的内容，如单页应用程序（SPA）和JavaScript生成的网页。
    -   **垂直爬虫**：垂直爬虫专注于收集特定类型的信息，例如医疗、教育、旅游等领域的数据。
2.  **按工作方式分类**：
    -   **单线程爬虫**：单线程爬虫是一次只能处理一个请求的爬虫，它们按顺序发送请求和处理响应。
    -   **多线程爬虫**：多线程爬虫使用多个线程来并行处理多个请求，以提高爬取速度。
    -   **分布式爬虫**：分布式爬虫将任务分配给多个计算节点，可以在不同机器上并行运行，以提高规模和效率。
3.  **按技术实现分类**：
    -   **基于HTTP的爬虫**：大多数爬虫使用HTTP协议来获取网页内容，通过HTTP请求和响应来交换数据。
    -   **无头浏览器爬虫**：无头浏览器爬虫模拟浏览器行为，包括JavaScript的执行，以处理动态网页。
    -   **API爬虫**：API爬虫专门用于从Web API中获取数据，通常以JSON或XML格式返回。
4.  **按合法性分类**：
    -   **合法爬虫**：合法爬虫遵守网站的robots.txt文件和使用政策，以获取数据并尊重网站的隐私和服务条款。
    -   **非法爬虫**：非法爬虫不遵守网站的规则和法律，可能会引起法律问题和网站的资源滥用。
5.  **按周期分类**：
    -   **定时爬虫**：定时爬虫按照固定的时间间隔执行，以获取更新的信息，例如新闻网站的头条。
    -   **实时爬虫**：实时爬虫几乎实时地监控网站的变化，以捕捉新内容，例如社交媒体上的帖子或推文。
