# 2.运行时的页面构建过程

## 第二章 运行时的页面构建过程

### 1\) 生命周期概览

浏览器构建了发送至服务器的请求，该服务器处理了请求并形成了一个通常由 HTML、CSS 和 JavaScript 代码所组成的响应。当浏览器接收了响应时，我们的客户端应用开始了它的生命周期。

生命周期执行步骤如下： 1. 页面构建-创建用户界面 2. 事件处理-进入循环从而等待事件的发生，发生后调用事件处理器。

### 2\) 页面构建阶段

两个步骤： 1. 解析HTML代码并构建文档对象模型（DOM） 2. 执行JavaScript代码

#### 1. HTML解析和DOM构建

1. 直到遇到第一个脚本元素，示例页面都在构建DOM
2. 浏览器会修复在蓝图中发现的问题，如`<head>`中错误包含了`<p>`，浏览器将静默修复错误，把`<p>`放在`<body>`元素中。

   **2. 执行JavaScript代码**

   脚本中的JavaScript代码由浏览器的JavaScript引擎执行，浏览器通过全局对象提供一个**API**时JavaScript引擎可以与浏览器交互并改变页面内容。

   **JavaScript中的全局对象**

   浏览器暴露的主要全局对象是window对象，代表包含着一个页面的窗口。其最主要属性是document，代表当前页面的DOM。

   **JavaScript代码的不同类型**

   全局代码和函数代码之分。

```markup
 <script>
        function addMessage(element,message){
            var messageElement = document.createElement("li");
            messageElement.textContent = message;
            element.appendChild(messageElement);
        }
        var first = document.getElementById("first");
        addMessage(first,"Page loading")
    </script>
```

**在页面构建阶段执行JavaScript代码**

**3.页面构建阶段遇到脚本节点，将停止构建，转而执行JavaScript代码。**

某个JavaScript代码执行期间用户创建的全局变量都能正常地被其他脚本元素中的JavaScript代码所访问到，因**全局`window`对象存在于整个页面的生存期间**。下面步骤在未处理完HTML和JavaScript前都会**交替执行**：

1. 将HTML构建为DOM
2. 执行JavaScript代码

处理完后，进入**事件处理**。

### 3\)事件处理

#### 1.事件处理概览

JavaScript为单线程执行模型，浏览器为跟踪已经发生但尚未处理的事件，使用了事件队列。

事件处理流程：

* 浏览器检查事件队列头；
* 如果浏览器没有在队列中检测到事件，则继续检查；
* 如果浏览器在队列头中检测到了事件，则取出该事件并执行相应的事件处理器 （如果存在）。在这个过程中，余下的事件在事件队列中耐心等待，直到轮到它们被处理。

放置事件的队列是在页面构建阶段和事件处理阶段以外的。这个过程对于决定事件何时发生并将其推入事件队列很重要，此过程不会参与事件处理线程。

**事件是异步的**

事件类型：

* 浏览器事件，诶如当页面加载完成后或无法加载时
* 网络事件，来自服务器的响应等
* 用户事件，鼠标单击
* 计时器事件

#### 2.注册事件处理器

* 把函数赋值给某个特殊属性

`window.onload = function(){};`

`document.body.onclick = function(){};`

缺点：对于某个事件只能注册一个事件处理器，可能会把上一个事件处理器改写掉。

* 使用内置`addEventListener`方法

#### 3.处理事件

