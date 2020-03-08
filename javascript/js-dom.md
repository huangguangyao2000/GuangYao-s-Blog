# index

## _**DOM**_

DOM（文档对象模型）是针对HTML和XML文档的一个API

## **节点层次**

* 文档节点是每个文档的根节点，文档节点只有一个子节点`<html>`，为**文档元素**。HTML页面中，文档元素始终都是`<html>`元素，在XML中，没有预定义的元素，任何元素都可能成为文档元素。

  **Node类型**

  DOM1 级定义了一个 Node 接口，该接口将由 DOM 中所有节点类型实现。

  节点类型有Node类型中定义的12个数值常量表示。

每个节点都有一个 nodeType 类型，

**节点关系**

**操作节点**

```javascript
appendChild()
//两个参数：要插入的节点和作为参照物的节点
var returnedNode = someNode.insertBefore(newNode,null);
//替换和被替换
var returnedNode = someNode.replacechild(newNode,someNode.firstChild);
//克隆
var deepList = myList.cloneNode(true);
//处理文档树上的文本节点
normalize()
```

### **Document类型**

document对象表示整个HTML页面，也是window对象的一个属性，可以将其作为全局对象访问。

#### 文档的子节点

访问Document节点子节点的快捷方式：

```markup
    <html>
        <body>
        </body>
    </html>
```

```javascript
var html = document.documentElement;
//html = document.childNodes[0]; //true
//html = document.firstChild; //true
```

document对象有一个body属性：

```javascript
var body = document.body;
```

通常将&lt;!DOCTYPE&gt;标签看成一个与文档其他部分不同的实体。

```javascript
var doctype = document.doctype;
```

#### 文档信息

标题

```javascript
var title = document.title;
document.title = 'hh';
```

网页请求相关

```javascript
//取得完整URL
var url = document.URL;
//取得域名
var domain = document.domain;
//取得来源页面的URL
var referrer = document.referrer;
```

domain属性可以实现跨域，但需要二级域名相同。

#### 查找元素

```javascript
var div = document.getElementById('myDiv');
var images = document.getElementsByTagName('img');
var myImage = images.nameItem("myItem");
var radios = document.getElementsByName("color");
```

#### DOM一致性检测

#### 文档写入

```javascript
//原样写入
write()
//在字符串末尾添加一个换行符
writeln()
//打开和关闭网页的输出流
open()和close()
```

### **Element类型**

#### HTML元素

每个HTML元素中都存在的下列标准特性：

* id，唯一标识符
* title，有关元素的附加说明
* className，为元素指定的css类名

  **取得特性**

  `getAttribute()`、`setAttribute()`、`removeAttribute()`

  **attributes属性**

* getNamedItem\(name\)
* removeNamedItem\(name\)
* setNamedItem\(node\)
* item\(pos\)

  **创建元素**

  `document.createElement()`

  ```javascript
  var div = document.createElement('div');
  document.body.appendChild(div);
  ```

  **元素的子节点**

  ```javascript
  var ul = documemnt.getElementById('myList');
  var li = ul.getElementsByTagName('li');
  ```

  **Text类型**

  **创建文本节点**

  ```javascript
  var textNode = document.createTextNode("<strong>Hello!</strong>");
  ```

  **Comment类型**

  注释

  ```javascript
  var div = document.getElementById("myDiv");
  var comment = div.firstChild;
  alert(comment.data);
  ```

  **DOM操作技术**

  **动态脚本**

* 插入外部文件

  ```markup
    <script type="text/javascript" src="client.js"></script>
  ```

* 直接插入代码

  ```javascript
  var script = document.createElement("script");
  script.type = "text/javascript";
  script.src = "client.js";
  ```

  **动态样式**

  ```markup
  <link rel="stylesheet" type="text/css" href="styles.css">
  ```

  ```javascript
  var link = document.createElement("link");
  link.rel = "stylesheet";
  link.type = "text/css";
  link.href = "style.css";
  var head = document.getElementsByTagName("head")[0];
  head.appendChild(link);
  ```

  加载外部样式文件的过程是**异步**的，也就是加载样式与执行JavaScript代码的过程没有固定的次序。

  **操作表格**

  **使用NodeList**

