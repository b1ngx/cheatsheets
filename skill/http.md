## 状态码

- 401
- 403

- 500


## OPTIONS 请求

1. 检测请求支持的 HTTP 方法, `curl -X OPTIONS http://example.org -i`

2. 在 CORS 中，可以使用 OPTIONS 方法发起一个预检请求，以检测实际请求是否可以被服务器所接受。预检请求报文中的 Access-Control-Request-Method 首部字段告知服务器实际请求所使用的 HTTP 方法。服务器从预检请求获得的信息来判断，是否接受揭晓来的请求。

参考：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS