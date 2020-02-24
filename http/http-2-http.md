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

