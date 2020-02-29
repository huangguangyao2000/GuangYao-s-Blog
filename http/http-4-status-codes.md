# HTTP-4-status-codes

## 告知请求结果

| 状态码 | 类别 | 原因 |
| :--- | :--- | :--- |
| 1xx | 信息状态码 | 接收的请求正在处理 |
| 2xx | 成功状态码 | 请求处理成功 |
| 3xx | 重定向状态码 | 需要附加信息操作才能完成 |
| 4xx | 客户端错误状态码 | 服务器端无法处理请求 |
| 5xx | 服务器端错误状态码 | 服务器处理请求错误 |

## 2XX

1. 200 OK：请求正常处理
2. 204 No Content：请求成功处理，但返回的响应报文中不包含实体的主体部分，也不允许返回任何实体的主体。
3. 206 Partial Content：客户端进行了范围请求，服务器成功执行了这部分GET请求。

## 3XX

1. 301 Move Permanently：永久性重定向
2. 302 Found：临时性重定向
3. 303 See Other：请求对应的资源存在另一个URI，应使用GET方法定向获取请求的资源。
4. 304 Not Modified：资源已找到，但不满足条件
5. 307 Temporary Redirect

## 4XX

1. 400 Bad Request：请求报文中存在语法错误。当错误发生时需修改请求的内容后再次发送请求。
2. 401 Unauthorized：第一次返回需认证，第二次返回为认证失败。
3. 403 Forbidden：访问被服务器拒绝。（可在主体部分描述原因，让用户看见）
4. 404 Not Found：服务器上没有请求的资源。

## 5XX

1. 500 Internet Server Error：服务器端执行请求时发生错误。
2. 503 Service Unavailable：服务器暂时处于超负载或正在进行停机维护，现在无法处理请求。
