# xpath解析

## 1. 最好用的解析！

-   xpath解析是最为通用的一个解析方式，通过层级访问精确找到需要解析的标签，在结构化数据中非常好用！
-   还记得lxml解析器吗? 我们在之前下载了它, 现在我们需要调用它的etree模块.
-   和bs4解析一样，我们需要实例化一个etree对象，并通过这个对象的属性和方法进行操作.
-   那为什么要叫xpath解析呢?
    -   XPath：XML Path Language，是一种用于XML文本的导航和选择的语言，顾名思义是用Path路径进行定位，同时提供了一些很好用的导航定位的方式．
    -   XPath可以通过节点名称或者位置进行导航，可以非常简单且精确定位到标签．

## 2. xpath语法

1.  **选择节点：**

    -   ```
        /   # 从根节点开始选择。
        ```

        -   例如：`/root/element` 选择根节点下的所有名为 "element" 的节点。

    -   ```
        //	# 从当前节点选择匹配选择的节点，而不考虑它们的位置。
        ```

        -   例如：`//element` 选择文档中的所有 "element" 节点。

2.  **按节点名称选择：**

    -   `element`：选择名称为 "element" 的所有元素。

    -   ```
        用*选择当前节点的所有子节点。
        ```

        -   例如：`/root/*` 选择根节点下的所有直接子节点。

    -   ```
        @attribute	# 选择当前节点的 attribute 属性。
        ```

        -   例如：`/root/element/@attribute` 选择根节点下名为 "element" 的节点的 "attribute" 属性。

3.  **按位置选择：**

    -   `element[1]`：选择当前节点下的第一个 "element" 子节点。
    -   `element[last()]`：选择当前节点下的最后一个 "element" 子节点。
    -   `element[position()<3]`：选择当前节点下的前两个 "element" 子节点。

4.  **按条件选择：**

    -   `element[@attribute='value']`：选择具有特定 attribute 值的 "element" 节点。
    -   `element[text()='text']`：选择具有特定文本内容的 "element" 节点。

5.  **通配符：**

    -   `*`：匹配任何元素节点。
    -   `@*`：匹配任何属性节点。

## 3. 理论成立，实践开始！

-   首先实例化这个HTML字符串成一个etree对象.

    ```py
    tree = etree.HTML(page_text)
    ```

-   然后调用这个对象的方法进行xpath解析.

    ```py
    r = tree.xpath('xpath表达式')
    ```

-   一些具体的定位操作如下

    ```
    # 查找div标签三种方式
    	r = tree.xpath('/html/body/div')   # '/'表示从根目录开始定位，层层定位
        r = tree.xpath('/html//div')	   # 1.'//'表示多个层级(中间有跳过中间层级)
        r = tree.xpath('//div')			   # 2.'//'表示任意查找
    # 通过属性定位标签
    	r = tree.xpath('//div[@class="tang"]') 		     # [ ]内，@为属性标识
        r = tree.xpath('//div[@class="tang"]//li[5]')    # xpath的下标不同列表，是【从1开始】
    # element对象取文本 ---> 【/text()和//text()】
        r = tree.xpath('//li[7]/a/text()')	  # /text()，标签内【直系】element对象转化为文本内容
        r = tree.xpath('//li[7]//text()')	  # //text()，标签内【所有】element对象转化为文本内容
    # element对象取属性 ---> 【/@attrName】
    	r = tree.xpath('//div[@class="song"]/img/@src')	  # img标签内的src属性值
    ```

-   同时xpath解析中还能通过逻辑运算符（and or ）进行定位．
-   更多的操作可以阅读官方文档（官方文档太难读，这里放个[好用的](https://cnblogs.com/my_captain/p/7490292.html)）



