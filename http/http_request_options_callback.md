<!-- YAML
added: v0.3.6
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->

* `options` {Object | string | URL}
  * `protocol` {string} 使用的协议。默认为 `http:`。
  * `host` {string} 请求发送至的服务器的域名或 IP 地址。默认为 `localhost`。
  * `hostname` {string} `host` 的别名。为了支持 [`url.parse()`]，`hostname` 优于 `host`。
  * `family` {number} 当解析 `host` 和 `hostname` 时使用的 IP 地址族。
    有效值是 `4` 或 `6`。当未指定时，则同时使用 IP v4 和 v6。
  * `port` {number} 远程服务器的端口。默认为 `80`。
  * `localAddress` {string} 为网络连接绑定的本地接口。
  * `socketPath` {string} Unix 域 Socket（使用 host:port 或 socketPath）。
  * `method` {string} 指定 HTTP 请求方法的字符串。默认为 `'GET'`。
  * `path` {string} 请求的路径。默认为 `'/'`。
    应包括查询字符串（如有的话）。如 `'/index.html?page=12'`。
    当请求的路径中包含非法字符时，会抛出异常。
    目前只有空字符会被拒绝，但未来可能会变化。
  * `headers` {Object} 包含请求头的对象。
  * `auth` {string} 基本身份验证，如 `'user:password'` 用来计算 `Authorization` 请求头。
  * `agent` {http.Agent | boolean} 控制 [`Agent`] 的行为。
    可能的值有：
   * `undefined` (默认): 对该主机和端口使用 [`http.globalAgent`]。
   * `Agent` 对象：显式地使用传入的 `Agent`。
   * `false`: 创建一个新的使用默认值的 `Agent`。
  * `createConnection` {Function} 当不使用 `agent` 选项时，为请求创建一个 socket 或流。
    这可以用于避免仅仅创建一个自定义的 `Agent` 类来覆盖默认的 `createConnection` 函数。详见 [`agent.createConnection()`]。
  * `timeout` {number}: 指定 socket 超时的毫秒数。
    它设置了 socket 等待连接的超时时间。
* `callback` {Function}
* 返回: {http.ClientRequest}

Node.js 为每台服务器维护多个连接来进行 HTTP 请求。
该函数允许显式地发出请求。

`options` 可以是一个对象、或字符串、或 [`URL`] 对象。
如果 `options` 是一个字符串，它会被自动使用 [`url.parse()`] 解析。
If it is a [`URL`][] object, it will be automatically converted to an ordinary `options` object.

可选的 `callback` 参数会作为单次监听器被添加到 [`'response'`] 事件。

`http.request()` 返回一个 [`http.ClientRequest`] 类的实例。
`ClientRequest` 实例是一个可写流。
如果需要通过 POST 请求上传一个文件，则写入到 `ClientRequest` 对象。

例子：

```js
const postData = querystring.stringify({
  'msg' : 'Hello World!'
});

const options = {
  hostname: 'www.google.com',
  port: 80,
  path: '/upload',
  method: 'POST',
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Content-Length': Buffer.byteLength(postData)
  }
};

const req = http.request(options, (res) => {
  console.log(`状态码: ${res.statusCode}`);
  console.log(`响应头: ${JSON.stringify(res.headers)}`);
  res.setEncoding('utf8');
  res.on('data', (chunk) => {
    console.log(`响应主体: ${chunk}`);
  });
  res.on('end', () => {
    console.log('响应中已无数据。');
  });
});

req.on('error', (e) => {
  console.error(`请求遇到问题: ${e.message}`);
});

// 写入数据到请求主体
req.write(postData);
req.end();
```

注意，在例子中调用了 `req.end()`。
使用 `http.request()` 必须总是调用 `req.end()` 来表明请求的结束，即使没有数据被写入请求主体。

如果请求过程中遇到任何错误（DNS 解析错误、TCP 级的错误、或实际的 HTTP 解析错误），则在返回的请求对象中会触发 `'error'` 事件。
对于所有的 `'error'` 事件，如果没有注册监听器，则抛出错误。

以下是需要注意的几个特殊的请求头。

* 发送 `'Connection: keep-alive'` 会通知 Node.js，服务器的连接应一直持续到下一个请求。

* 发送 `'Content-Length'` 请求头会禁用默认的块编码。

* 发送 `'Expect'` 请求头会立即发送请求头。
  通常情况下，当发送 `'Expect: 100-continue'` 时，超时时间与 `continue` 事件的监听器都需要被设置。
  详见 RFC2616 章节 8.2.3。

* 发送 `Authorization` 请求头会替代 `auth` 选项计算基本身份验证。

Example using a [`URL`][] as `options`:

```js
const { URL } = require('url');

const options = new URL('http://abc:xyz@example.com');

const req = http.request(options, (res) => {
  // ...
});
```

