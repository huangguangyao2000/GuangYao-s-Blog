# HTTP-2-HTTP

## HTTP协议用于客户端和服务器端之间的通信

## 通过请求和响应的交换进行通信

* 请求从客户端发出,最后服务器端相应应该请求并返回
* **请求报文**

```text
POST /index.htm HTTP/1.1  // 请求方法 / 请求访问的资源对象(请求URI) / HTTP版本号

// 请求首部字段
Host: hackr.jp
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length:16

// 内容实体
name=ueno&age=37
```

* 响应报文

```text
HTTP/1.1 200 OK  //协议版本 状态码 状态码的原因短语

//响应首部字段
Date: Tue,10 Jul 2012 06:50:15 GMT 
Content-Length:362
Content-Type:text/html

//主体
<html>
...
```

## HTTP 是不保存状态的协议

* 无状态\(stateless\)协议,协议自身不对请求和响应之间的通信状态进行保存,不做持久化处理
* 现此特性成了约束,用cookies来解决此问题

## 请求 URI 定位资源

### 请求方式

* URL为完整的请求URI

```text
GET http://hackr.jp/index.htm HTTP/1.1
```

* 在首部字段Host中写明网络域名或IP地址

```text
GET /index.htm HTTP/1.1
Host:hackr.jp
```

* 对服务器本身发起请求可用\*来代替URI

```text
OPTIONS * HTTP/1.1
```

## HTTP方法

### GET：获取资源

* 用来请求访问已被URI识别的资源

### POST:传输实体主体

### PUT:传输文件

* 有安全性问题

### HEAD:获得报文首部

与GET一样，但不返回报文主体部分。用于确认URI的有效性和资源更新的截止日期时间等。

### DELETE:删除文件

本身和 PUT 方法一样不带验证机制

### OPTIONS：询问支持的方法

查询针对请求 URI 指定的资源支持的方法

### TRACE：追踪路径

让 Web 服务器端将之前的请求通信返回给客户端的方法。它容易引发 XST

### CONNECT：要求用隧道协议连接代理

求在与代理服务器通信时建立隧道，实现用隧道协议进行 TCP 通信。

## 使用方法下达命令

## 持久连接节省通信量

### 持久连接

**HTTP/1.1** 和一部分的 **HTTP/1.0** 想出了**持久连接**（HTTP Persistent Connections，也称为 HTTP keep-alive 或 HTTP connection reuse）

* 特点是，只要任意一端没有明确提出断开连接，则保持 TCP 连接状态。
* **在 HTTP/1.1 中，所有的连接默认都是持久连接**，但在 HTTP/1.0 内并未标准化。



