<!-- YAML
added: v0.3.6
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: The `url` parameter can now be passed along with a separate
                 `options` object.
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->

* `url` {string | URL}
* `options` {Object}
  * `protocol` {string} 使用的协议。**默认值:** `'http:'`。
  * `host` {string} 请求发送至的服务器的域名或 IP 地址。**默认值:** `'localhost'`。
  * `hostname` {string} `host` 的别名。为了支持 [`url.parse()`]，如果同时指定 `host` 和 `hostname`，则使用 `hostname`。
  * `family` {number} 当解析 `host` 或 `hostname` 时使用的 IP 地址族。有效值为 `4` 或 `6`。如果没有指定，则同时使用 IP v4 和 v6。
  * `port` {number} 远程服务器的端口。**默认值:** `80`。
  * `localAddress` {string} 为网络连接绑定的本地接口。
  * `socketPath` {string} Unix 域套接字。如果指定了 `host` 或 `port` 之一（它们指定了 TCP 套接字），则不能使用此选项。
  * `method` {string} 一个字符串，指定 HTTP 请求的方法。**默认值:** `'GET'`。
  * `path` {string} 请求的路径。应包括查询字符串（如果有）。例如 `'/index.html?page=12'`。当请求的路径包含非法的字符时，则抛出异常。目前只有空格被拒绝，但未来可能会有所变化。**默认值:** `'/'`。
  * `headers` {Object} 包含请求头的对象。
  * `auth` {string} 基本的身份验证，即 `'user:password'`，用于计算授权请求头。
  * `agent` {http.Agent | boolean} 控制 [`Agent`] 的行为。可能的值有：
    * `undefined` (默认): 对此主机和端口使用 [`http.globalAgent`]。
    * `Agent` 对象: 显式地使用传入的 `Agent`。
    * `false`: 使用新建的具有默认值的 `Agent`。
  * `createConnection` {Function} 当 `agent` 选项未被使用时，用来为请求生成套接字或流的函数。这可用于避免创建自定义的 `Agent` 类以覆盖默认的 `createConnection` 函数。详见 [`agent.createConnection()`]。任何[双工流][`Duplex`]都是有效的返回值。
  * `timeout` {number}: 指定套接字超时的数值，以毫秒为单位。这会在套接字被连接之前设置超时。
  * `setHost` {boolean}: 指定是否自动添加 `Host` 请求头。**默认值:** `true`。
* `callback` {Function}
* 返回: {http.ClientRequest}

Node.js 为每个服务器维护多个连接以发出 HTTP 请求。
此函数允许显式地发出请求。

`url` 可以是字符串或 [`URL`] 对象。
如果 `url` 是一个字符串，则会自动使用 [`url.parse()`] 解析它。
如果它是一个 [`URL`] 对象，则会自动转换为普通的 `options` 对象。

如果同时指定了 `url` 和 `options`，则对象会被合并，其中 `options` 属性优先。

可选的 `callback` 参数会作为单次监听器被添加到 [`'response'`] 事件。

`http.request()` 返回 [`http.ClientRequest`] 类的实例。 
`ClientRequest` 实例是一个可写流。
如果需要使用 POST 请求上传文件，则写入到 `ClientRequest` 对象。

```js
const postData = querystring.stringify({
  'msg': '你好世界'
});

const options = {
  hostname: 'nodejs.cn',
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
    console.log('响应中已无数据');
  });
});

req.on('error', (e) => {
  console.error(`请求遇到问题: ${e.message}`);
});

// 将数据写入请求主体。
req.write(postData);
req.end();
```

注意，在示例中调用了 `req.end()`。
使用 `http.request()` 时，必须始终调用 `req.end()` 来表示请求的结束，即使没有数据被写入请求主体。

如果在请求期间遇到任何错误（DNS 解析错误、TCP 层的错误、或实际的 HTTP 解析错误），则会在返回的请求对象上触发 `'error'` 事件。
与所有 `'error'` 事件一样，如果没有注册监听器，则会抛出错误。

以下是需要注意的一些特殊的请求头。

* 发送 `'Connection: keep-alive'` 会通知 Node.js 与服务器的连接应该持续到下一个请求。

* 发送 `'Content-Length'` 请求头会禁用默认的分块编码。

* 发送 `'Expect'` 请求头会立即发送请求头。通常情况下，当发送 `'Expect: 100-continue'` 时，应设置超时时间和 `'continue'` 事件的监听器。详见 RFC2616 的第 8.2.3 节。

* 发送授权请求头会使用 `auth` 选项覆盖以计算基本的身份验证。

使用 [`URL`] 作为 `options` 的示例：

```js
const options = new URL('http://abc:xyz@nodejs.cn');

const req = http.request(options, (res) => {
  // ...
});
```

在成功的请求中，会按以下顺序触发以下事件：

* `'socket'` 事件
* `'response'` 事件
  * `res` 对象上任意次数的 `'data'` 事件（如果响应主体为空，则根本不会触发 `'data'` 事件，例如在大多数重定向中）
  * `res` 对象上的 `'end'` 事件
* `'close'` 事件

如果出现连接错误，则触发以下事件：

* `'socket'` 事件
* `'error'` 事件
* `'close'` 事件

如果在连接成功之前调用 `req.abort()`，则按以下顺序触发以下事件：

* `'socket'` 事件
* (在这里调用 `req.abort()`)
* `'abort'` 事件
* `'error'` 事件并带上错误信息 `'Error: socket hang up'` 和错误码 `'ECONNRESET'`
* `'close'` 事件

如果在响应被接收之后调用 `req.abort()`，则按以下顺序触发以下事件：

* `'socket'` 事件
* `'response'` 事件
  * `res` 对象上任意次数的 `'data'` 事件
* (在这里调用 `req.abort()`)
* `'abort'` 事件
* `res` 对象上的 `'aborted'` 事件
* `'close'` 事件
* `res` 对象上的 `'end'` 事件
* `res` 对象上的 `'close'` 事件

注意，设置 `timeout` 选项或使用 `setTimeout()` 函数不会中止请求或执行除添加 `'timeout'` 事件之外的任何操作。
