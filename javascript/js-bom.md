# JS-BOM

## window对象

* 通过JS访问浏览器窗口的一个接口
* 又是ES规定的Global对象。

  **全局作用域**

* 全局变量可以成为window对象的属性。
* 全局变量不能通过delete操作符删除，而直接声明在window对象上的属性可以。
* IE8及更早版本，不管来源，只要用delete删除全局变量，便报错。

  **窗口关系及框架**

  每个框架都拥有自己的window对象，并保存在frames集合中，可通过索引或框架名称来访问相应的window对象。

  **窗口位置**

  ```javascript
  screenLeft
  screenTop
  screenX
  screenY
  （不同浏览器可能不同）
  //确定需要跨浏览器时，可使用如下代码：
  var leftPos = (typeof window.screenLeft == 'number')?window.screenLeft:window.screenX;
  moveTo()
  moveBy()
  ```

  **窗口大小**

  ```javascript
  innerWidth innerHeight outerWidth outerHeight
  document.documentELement.clientWidth
  document.documentELement.clientHeight
  document.body.clientHeight
  document.body.clientWidth
  resizeTo()
  resizeBy()
  ```

  **location对象**

  既为window对象的属性，还是document对象的属性。

### 用处：

* 保存着当前文档的信息。
* 将URL解析为独立的片段。

| hash | 回URL中hash（\#所跟部分） |
| :--- | :--- |
| host | 返回服务器名称和端口号 |
| hostname | 返回服务器名称 |
| href | 返回当前加载页面的完整URL，location对象的toString\(\)方法也返回此值 |
| pathname | 返回URL中的目录和文件名 |
| port | 返回端口号 |
| protocal | 返回协议名 |
| search | 返回URL的查询字符串 |

### 查询字符串

### 位置操作

```javascript
location.assign("http://www.xxx.com");
```

可立即打开新URL并在浏览器历史记录中生成一条记录。

```javascript
location.replace("http://www.xxx.com");
location.reload(); //重新加载（有可能从缓存中加载）
location.reload(true); //重新加载（从服务器重新加载）
```

## history对象

```javascript
//负退 正进 或直接跳转
history.go(-1);

//后退
history.back();
//前进
history.forward();
//保存的历史记录的数量
history.length();
```

