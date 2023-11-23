# bs4解析

## 1. 一些事先了解

-   需要实例化一个BeautifulSoup对象，将爬取到的数据加载到对象中，通过这个对象的一些属性和方法，对对象中的数据进行处理．

-   在这种解析方式中，我们需要导入第三方库bs4中的BuautifulSoup模块，用pip进行下载.

    ```py
    pip install bs4
    ```

-   同时我们需要用lxml解析器（后续xpath解析也会用到），同样用pip进行下载.

    ```py
    pip install lxml
    ```

-   解析器：分析和解释结构化的数据，让其变得更容易处理．
-   和re模块一样，BeautifulSoup模块中也提供了很多属性和方法供我们使用，常见的如下：
    -   soup.tagName：只返回第一个tagName标签.
    -   soup.find( 'tagName', class_ = '属性值' )：只返回第一个tagName标签.
    -   soup.find_all( 'tagName' )：返回所有tagName标签.
    -   soup.select( '某种选择器 (id, class, 标签 )' )：windows系统不支持.
    -   更多的BeautifulSoup提供的对象方法可见页尾或官方文档.

## 2. 让我们小试牛刀

```py
import requests
from bs4 import BeautifulSoup
# fp = open('text.html','r',encoding='utf-8')
# soup = BeautifulSoup(fp,'lxml')
text = requests.get(url,data,headers).text
soup = BeautifulSoup(text,'lxml')
print(soup.find_all('div'))
```

-   上述程序中先导入了bs4中的BeautifulSoup模块，同时新建了一个BeautifulSoup实例化对象soup.
-   我们通过这个实例化对象提供的方法`find_all`解析了所有这个html文档中的div标签.
-   如果想要更加更加精确和深入的解析想要的标签，得通过更复杂的CSS选择器或者标签的class和id等属性来精确定位.

## 3. 附带一些常用函数

1. **BeautifulSoup 对象的基本用法：**
   - `BeautifulSoup(markup, 'html.parser')`：用于创建一个 BeautifulSoup 对象，其中 `markup` 是要解析的HTML或XML文档，而 `'html.parser'` 是指定解析器的名称。

2. **标签(Tag)对象的方法：**
   - `tag.name`：获取标签的名称。
   - `tag.contents`：获取标签的子节点列表。
   - `tag.parent`：获取标签的父节点。
   - `tag.find(name, attrs, recursive, string)`：查找第一个符合条件的子节点。
   - `tag.find_all(name, attrs, recursive, string)`：查找所有符合条件的子节点。

3. **搜索文档的方法：**
   - `find(name, attrs, recursive, string)`：在文档中查找第一个符合条件的标签。
   - `find_all(name, attrs, recursive, string)`：在文档中查找所有符合条件的标签。
   - `select(css_selector)`：通过 CSS 选择器查找标签。

4. **标签对象的属性和方法：**
   - `tag['attribute']`：获取标签的属性值。
   - `tag.get('attribute')`：获取标签的属性值，如果属性不存在则返回 None。
   - `tag.attrs`：获取标签的所有属性。
   - `tag.string`：获取标签内的文本内容。

5. **修改文档的方法：**
   - `tag.replace_with(new_tag)`：用新标签替换当前标签。
   - `tag.decompose()`：移除当前标签及其所有子节点。
   - `tag.insert(position, new_tag)`：在指定位置插入新标签。
   - `tag.append(new_tag)`：在标签末尾添加新标签。
   - `tag.extract()`：将标签提取出来，从文档中移除。

6. **NavigableString 对象的方法：**
   - `NavigableString` 用于表示标签内的文本内容。
   - `string.replace_with(new_string)`：用新的文本内容替换当前文本内容。

这些方法提供了丰富的功能，使得 Beautiful Soup 在处理和解析 HTML 或 XML 文档时变得非常灵活和方便。你可以根据具体的需求选择适当的方法来提取或操作文档中的信息。更多的bs4模块的用法你可以访问[官方文档](https://beautifulsoup.readthedocs.io/zh-cn/v4.4.0/)（Hit it）.

