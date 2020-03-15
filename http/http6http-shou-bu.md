# HTTP6-HTTP首部

## HTTP6-HTTP首部

### HTTP报文首部

* 报文首部
* 空行
* 报文主体

必定包含HTTP首部，客户端和服务器端分别处理请求和响应提供所需要的信息。

#### HTTP请求报文

```javascript
GET / HTTP/1.1
Host: hackr.jp
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:13.0) Gecko/20100101 Firefox/13.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*; q=0.8
Accept-Language: ja,en-us;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Connection: keep-alive
If-Modified-Since: Fri, 31 Aug 2007 02:02:20 GMT
If-None-Match: "45bae1-16a-46d776ac"
Cache-Control: max-age=0
```

#### HTTP响应报文

```text
HTTP/1.1 304 Not Modified
Date: Thu, 07 Jun 2012 07:21:36 GMT
Server: Apache
Connection: close
Etag: "45bae1-16a-46d776ac"
```

### HTTP首部字段

#### 传递信息

为浏览器和服务器提供报文主体大小,所使用语言,认证信息等内容

#### HTTP首部字段结构

```text
首部字段名：字段值
```

```text
Content-Type: text/html
```

#### 四种首部字段类型

以在前面图片中说明

#### 常见首部

**请求首部**：Accept可接收媒体资源的类型，Accept-Charset可接收的字符集，Host请求的主机名。

**响应首部**：ETag资源的匹配信息，Location客户端重定向的URI

**通用首部**：Cache-Control控制缓存策略，Connection管理持久连接。

**实体首部**：Content-Length实体主体的大小，Expires实体主体的过期时间、Last-Modified资源最后修改时间。

#### HTTP/1.1首部字段

#### 非HTTP/1.1首部字段

Set-cookies和Cookie,Content-Disposition等

### HTTP/1.1协议缺点

默认使用持久连接，多个请求可以复用同一个TCP连接，但是在同一个TCP连接中，数据请求的通信次序是一定的。服务器只有处理完一个请求的响应后，才能处理下一个请求。若前面的处理太慢，则会造成堵塞，称为“队头堵塞”。

减少请求数，同时打开多个持久连接都能解决此问题。

### HTTP/2

特性

* 二进制协议

HTTP/2是一个二进制协议。头信息和数据体都是二进制，并且统称为帧。

* 多路复用

仍然复用TCP连接，但是在一个连接里，客户端和服务器都可以同时发送多个请求与响应，且不用按次序一一发送。

* 数据流

将每个请求或响应的所有数据包，称为一个数据流。每个数据流都有独特的编号。数据流发送时都必须标记数据流ID。

* 头信息压缩

gzip或compress压缩后再发送。客户端和服务器都会同时维护一张头信息表，所有字段都会存入这个表，生成一个索引号，以后就不发送同样字段了，只发送索引号

* 服务器推送

允许服务器未经请求，主动向客户端发送资源，叫做服务器推送。

