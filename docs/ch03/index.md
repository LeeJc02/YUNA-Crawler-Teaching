# 最简单的爬虫小案例分析

## 1. 发生了甚么!

-   我们刚刚发生了甚么事, 怎么三行代码跑出来了这么多东西! 

-   让我们首先来看得到的结果

```python
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

-   从前面讲过的前端基础我们可以知道这是一段**HTML代码**, 是这个`https://bilibili.com`网址的源代码, 我们不妨把源程序展开

```python
import requests
response = requests.get('https://bilibili.com').text
print(response)
```

```python
import requests					# 导入requests模块用于调用里面的函数
url = 'https://bilibili.com'	# 需要解析的URL
response = requests.get(url)    # 通过requests.get函数, 我们拿到了一个请求类型为get的响应对象
print(response.text)			# 将该对象的类型转换为文本得到了响应的内容, 为这个网页的HTML源代码
```

## 2. 好像有点简单(●ˇ∀ˇ●)

-   我们通过requests.get函数, 模拟真人访问该url, 就得到了访问该url的响应数据包

-   为什么是get呢, 前文讲了, get是**用于获取**, 第一次打开一个网页自然应该是获取而不是修改增加删除什么的

-   这个时候我们试试加一串代码

```python
print(requests.status_code)		# 成功打印出状态返回值为200, 则说明访问成功
```

## 3. 第一次写的代码怎么能不存起来?

1.   爬虫爬取的数据一般用于保存或者计算, 接下来我们把第一次爬取的HTML保存起来

```python
with open('./theFirst.html','w',encoding='UTF-8') as fp:
    fp.write(response.text)
```

2.   `with open`语句用于打开一个文件 (我记得这个语句原理上挺复杂的, 感兴趣的童鞋可以去了解一下)
3.   `./`表示在本级目录下, `../`表示上一级目录, `/`表示根目录
4.   `theFirst`为存储的文件名, `.html`是文件后缀名, 表示以html的格式保存
5.   `w`表示只写, 若文件不存在则自动创建文件
6.   `encoding`表示解码以`UTF-8`编码进行解码  (得到的东西都是二进制, 需要逆向还原成文本)
7.   `as fp`表示以叫做fp的**文件对象**打开, `fp.write`写入

## 锵锵! 这样你就将爬取的代码保存到目录的文件里了!

```python
# 示例代码
import requests
response = requests.get('https://bilibili.com').text
if (requests.status_codes != 200):
    print("Error")
with open('./theFirst.html', 'w', encoding='UTF-8') as fp:
    fp.write(response)
```

