
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

要使用 HTTP 服务器与客户端，可以 `require('http')`。

Node.js 的 HTTP 接口支持协议的多种特性。
接口不缓冲完整的请求或响应，应以流的形式处理数据。

HTTP 消息头表现为一个对象，例如：

<!-- eslint-skip -->
```js
{ 'content-length': '123',
  'content-type': 'text/plain',
  'connection': 'keep-alive',
  'host': 'mysite.com',
  'accept': '*/*' }
```

键名是小写的，键值不能修改。

为了支持各种可能的 HTTP 应用，Node.js 的 HTTP 接口都是非常底层的，只处理流与解析消息。
接口会将消息解析成消息头和消息主体，但不解析具体的消息头或消息主体。

查看 [`message.headers`] 了解如何处理重复的消息头。

接收到的原始消息头保存在 `rawHeaders` 属性中，它是一个 `[key, value, key2, value2, ...]` 数组。
例如，上面的消息头对象对应的 `rawHeaders` 如下：

<!-- eslint-disable semi -->
```js
[ 'ConTent-Length', '123456',
  'content-LENGTH', '123',
  'content-type', 'text/plain',
  'CONNECTION', 'keep-alive',
  'Host', 'mysite.com',
  'accepT', '*/*' ]
```

