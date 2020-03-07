# JS-客户端检测

## 客户端检测

### 能力检测

* 最广泛接受的客户端检测方式
* 不是识别特定的浏览器，而是识别浏览器的能力。

检测是否支持id获取方法：

```javascript
function getElement(id){
 if (document.getElementById){
 return document.getElementById(id);
 } else if (document.all){
 return document.all[id];
 } else {
 throw new Error("No way to retrieve element!");
 }
}
```

#### 更可靠的能力检测

上文为确定对象是否存在，但仍不清楚是不是我们所要的对象。

```javascript
//只检测了是否存在sort方法
function isSortable(object){
    return !!object.sort;
}

//检测sort是否为函数更合理
function isSortable(object){
    return typeof object.sort == "function";
}
```

尽量使用typeof进行能力检测。

#### 能力检测不是浏览器检测

## 怪癖检测

怪癖检测的目标是识别浏览器的特殊行为。主要是想知道浏览器存在什么缺陷。通常需要用代码来检测特性能否正常工作。

## 用户代理检测

通过检测用户代理字符串来确定实际使用的浏览器。

在每次 HTTP 请求中，用户代理字符串是作为响应首部发送的，可通过`nevigator.userAgent`属性访问。

### 用户代理字符串检测技术

```javascript
ie版本检测
if(IeVer>=6){
    //代码
}
```

