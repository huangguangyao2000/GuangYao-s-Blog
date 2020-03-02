# 各种问题

### html语义化

1. 少用`<div>`和`<span>`,在语义不明显时，使用`<p>`标签
2. 不用纯样式标签如`<font>`,`<u>`
3. 表格各部分使用对应标签
   1. `<caption>`-标题
   2. `<thread>`-主体
   3. `<tfoot>`-尾部
   4. `<th>`-表头
   5. `<td>`-单元格
4. 表单域用`<fieldset>`标签包围，并用legend标签说明表单用途
5. input标签对应都要有label标签说明

### 几种获得宽度和高度的方式

* dom.style.width
* dom.currentStyle.width
* window.getComputedStyle\(\).width
* window.getBoundingClientRect\(\).width\(\)
* dom.offsetWidth\(\)

### 各种获得宽高的方式

* window.screen.height
* window.screen.availHeight
* document.body.scrollHeight
* document.body.scrollTop/scrollLeft
* document.body.clientHeight
* document.body.offsetHeight

### CSS居中方法

#### 水平方向

```css
.text_div{
    text-align:center;
}
```

```css
.text_div{
    margin:0 auto;
}
```

```css
.wrap{
    float:left;
    position:relative;
    left:50%;
    clear:both;
}
.wrap-center{
    left:-50%;
}
```

#### 垂直方向

```css
.text_div{
    height:80px
    line-height:80px;
}
```

```css
.father{
    display:table;
}
.childern{
    display:table-cell;
    vertical-align:middle;
    text-align:center;
}
```

```css
.center-flex{
    display:flex;
    flex-direction:column;
    justify-content:center;
}
```

```css
.parent{
    position:relative;
}
.clildren{
    position:absolute;
    top:50%;
    margin-top:-50px;
    height:100px;
}
```

```css
.parent{
    position:relative;
}
.children{
    position:absolute;
    top:50%;
    transform:translateY(-50%);
}
```

水平垂直居中

```css
.parent{
    display:flex;
    justify-content:center;
    align-items:center;
}
```

```css
.parent{
    display:grid;
    height:140px;
}
.children{
    margin:auto
}
```

### display

* inline
* block
* flex
* grid
* inline-block
* inherit
* table

### XSS\(跨站脚本攻击\)

XSS\(跨站脚本攻击\)，恶意的注入html代码，其他用户访问时，会被执行

#### 特点：

能注入恶意的HTML/JavaScript代码到用户浏览的网页上，从而达到Cookie资料窃取、会话劫持、钓鱼欺骗等攻击

#### 防御手段：

* 浏览器禁止页面的JS访问带有HttpOnly属性的Cookie
* 两端进行**输入格式检查**
* 通过编码转义的方式进行输出检查

  **CSRF\(攻击跨站请求伪造\)**

  **特点：**

  重要操作的所有参数都是可以被攻击者猜测到的。攻击者预测出URL的所有参数与参数值，才能成功地构造一个伪造的请求。

  **防御手段：**

* token验证机制，比如请求数据字段中添加一个token，响应请求时校验其有效性
* 用户操作限制，比如验证码（繁琐，用户体验差）
* 请求来源限制，比如限制HTTP Referer才能完成操作（防御效果相比较差）

### 跨域

#### JSONP

JSON with Padding，用于解决主流浏览器的跨域数据访问问题。

主要利用Web页面调用js文件不受同源策略的限制。

1. 前端设置回调函数，并将其作为url的参数。
2. 服务器端接受到请求后，通过该参数获得回调函数名，并将数据放在参数中将其返回。
3. 收到为`<scipt>`标签。浏览器把它当作脚本来运行。

```javascript
//server.js
const url = require('url');
require('http').createServer((req,res)=>{
    const data={
        x:10
    }
    const callback = url.parse(req.url,ture).query.callback;
    res.writeHead(200);
    res.end('${callback}(${JSON.stringfy(data)')
}).listen(3000,'127.0.0.1');
```

```markup
<!--html-->
<body>
    <script>
        function jsonCallback(data){
            alert('获得数据'+data.x)
        }
    </script>
    <script src="http://127.0.0.1:3000?callback=jsonCallback"></script>
<body>
```

**优点**

* 兼容性好
* 不需XMLHttpRequest或ActiveX的支持；并且在请求完毕后可以通过调用callback方式回传结果

  **缺点**

* 只支持GET请求
* 只支持跨域HTTP请求的情况。不能解决不同域的两个页面或iframe之间进行数据通信的问题

#### CORS

W3C标准——跨域资源共享\(cross-origin resource sharing\)

允许浏览器向跨源服务器发出XMLHttpRequest请求，克服Ajax只能同源使用的局限。

需要浏览器和服务器同时支持才生效。关键是服务器实现CORS接口。

```markup
<script>
    const xhr = new XMLHttpRequest();
    xhr.open('GET','http://127.0.0.1:3000',true);
    xhr.onreadystatechange = function(){
        if(xhr.readyState===4 && xhr.status === 200){
            alert(xhr.responseText);
        }
    }
    xhr.send(null);
</script>
```

```javascript
require('http').createServer((req,res)=>{
    res.writeHead(200,{
        'Access-Control-Allow-origin':'http://localhost:8080'
    });
    res.end('这是你要的数据')
}).listen(3000,'127.0.0.1');

console.log('启动服务')
```

**优点**

1. 使用方便，更为安全
2. 支持POST请求方式
3. 兼容性问题，仅支持IE10以上

### Node Event Loop:6个阶段

* timer阶段：执行到期的setTimeout/setInterval队列回调
* I/O阶段：执行上轮循环残留的callback
* idle,prepare
* poll:等待回调
  * 执行回调
  * 执行定时器
    * 如有到期setTimeout/setInterval，则返回timer阶段
    * 如有setImmediate，则前往check阶段
* check
  * 执行setImmediate
* close callback

### 浏览器下的事件循环

执行一个宏任务，然后执行清空微任务列表，循环再执行宏任务，再清微任务列表。

微任务 microtask\(jobs\): promise / ajax / Object.observe\(该方法已废弃\)

宏任务 macrotask\(task\): setTimout / script / IO / UI Rendering

### babel编译原理

* babylon 将 ES6/ES7 代码解析成 AST
* babel-traverse 对 AST 进行遍历转译，得到新的 AST
* 新 AST 通过 babel-generator 转换成 ES5

### AST

抽象语法树 \(Abstract Syntax Tree\)，是将代码逐字母解析成 树状对象 的形式

### 拷贝

#### 浅拷贝

* Object.assign
* ...展开运算符

  **深拷贝**

* 递归进行赋值
* JSON.parse\(JSON.stringfy\(obj\)\):性能最快
  * 具有循环引用的对象时，报错
  * 当值为函数，symbol或undifined无法拷贝

### http/https 协议

#### 1.0 协议缺陷:

* 无法复用链接，完成即断开，重新慢启动和 TCP 3次握手
* head of line blocking: 线头阻塞，导致请求之间互相影响

  **1.1 改进:**

* 长连接\(默认 keep-alive\)，复用
* host 字段指定对应的虚拟站点
* 新增功能:
  * 断点续传
  * 身份认证
  * 状态管理
  * cache 缓存
    * Cache-Control
    * Expires
    * Last-Modified
    * Etag

### transition和animation的区别

#### 触发方式

前者作为某一变化的反应，譬如使用:hover伪类触发的过渡效果。 后者animation动画无需任何显式的触发，一旦定义动画，将自动播放

#### 循环

transition当触发时，一般只能运行一次。animation的循环可通过设置animation-iteration-count产生。

#### 定义中间点/关键帧

animation动画可以定义关键帧。transition只有start和end

### 使元素消失的办法

* visibility:hidden：隐藏，不改变布局，不会触发事件
* display:none：元素隐藏，会改变布局
* z-index:-1
* opacity:0:元素隐藏，不改变布局，可触发事件

### 前端储存

#### 常见存储方式

1. indexBD: h5的本地存储库，没网络浏览器也可以从这里读取数据，离线运用。5mb
2. Cookie:记录信息确认用户身份，最大4kb,这也就限制了传输的数据，请求的性能会受到影响 
3. Session:**服务器端**使用的一种记录客户状态的机制
4. localStroage: h5的本地存储，数据永久保存在**客户端**，chrome中2.6mb

   **区别**

5. 浏览器和服务器之间仅需传递session id即可，服务器根据session-id找到对应的用户session对象.
6. cookie数据始终在同源的http请求中携带，在浏览器和服务器来回传递，里面存放着session-id
7. cookie在设置的（服务器设置）有效期内有效，不管窗口和浏览器关闭，sessionStorage仅在当前浏览器窗口关闭前有效，关闭即销毁（临时存储）

   ```text
   localStorage始终有效    
   ```

### token、cookie、session三者的理解

1. token为令牌，为用户身份认证方式
2. cookie就是在客户端上的一个包括登陆信息等内容的文件。
3. session是一类用来保存客户端与服务器端之间状态的解决方案，会话完成后将被销毁。

#### 延申——session与token区别

1. session认证只是把简单的session信息存储在Session里面，sessionID不可预测.只存在于服务端.
2. token是oAuth Token,提供的是认证和授权,认证针对用户,授权针对应用.token是唯一的不能转移到其他应用或用户上.存在于客户端.

