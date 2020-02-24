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

* **无状态**\(stateless\)协议,协议自身不对请求和响应之间的通信状态进行保存,不做**持久化处理**
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

**HTTP/1.1** 和部分 **HTTP/1.0 有持久连接**（HTTP keep-alive）

* 任意一端没有断开则保持连接。
* **HTTP/1.1 默认持久连接**，但HTTP/1.0 内未标准化。

### 管线化——（pipelining）

**并行发送**请求

## Cookie 的状态管理

在请求和响应报文中写入 Cookie 信息来控制客户端的状态

* 响应报文Set-Cookie的首部字段信息，通知客户端保存Cookie。下次请求报文会加入Cookie值，然后服务器检查Cookie来源，对比服务器上的信息，得到状态信息。

### 交互场景

1. 请求报文（没有 Cookie 信息的状态）

   ```text
   GET /reader/ HTTP/1.1
   Host: hackr.jp
   ```

2. 首部字段内没有Cookie的相关信息
3. 响应报文（服务器端生成 Cookie 信息）

   ```text
   HTTP/1.1 200 OK
   Date: Thu, 12 Jul 2012 07:12:20 GMT
   Server: Apache
   ＜Set-Cookie: sid=1342077140226724; path=/; expires=Wed,
   10-Oct-12 07:12:20 GMT＞
   Content-Type: text/plain; charset=UTF-8
   ```

4. 请求报文（自动发送保存着的 Cookie 信息）

   ```text
   GET /image/ HTTP/1.1
   Host: hackr.jp
   Cookie: sid=1342077140226724
   ```

