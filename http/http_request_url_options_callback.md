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
  * `protocol` {string} 使用的协议。默认为 `http:`。
  * `host` {string} 服务器的域名或 IP 地址。默认为 `localhost`。
  * `hostname` {string} `host` 的别名。为了支持 [`url.parse()`]，`hostname` 优先于 `host`。
  * `family` {number} 解析 `host` 和 `hostname` 时使用的 IP 地址族。值可以是 `4` 或 `6`。如果没有指定，则同时使用 IP v4 和 v6。
  * `port` {number} 远程服务器的端口。默认为 `80`。
  * `localAddress` {string} 网络连接绑定的本地接口。
  * `socketPath` {string} Unix 域 Socket。`host:port` 或 `socketPath` 二选一。
  * `method` {string} 请求的方法。默认为 `'GET'`。
  * `path` {string} 请求的路径。可以包括查询字符串，如 `'/index.html?page=12'`。如果请求的路径中包含非法字符，则抛出异常。默认为 `'/'`。
  * `headers` {Object} 请求头。
  * `auth` {string} 基本身份验证，如使用 `'user:password'` 计算 `Authorization` 请求头。
  * `agent` {http.Agent | boolean} 控制 [`Agent`] 的行为。可选的值有：
    * `undefined` (默认): 使用 [`http.globalAgent`]。
    * `Agent`: 使用传入的 `Agent`。
    * `false`: 新建一个使用默认配置的 `Agent`。
  * `createConnection` {Function} 如果没有指定 `agent`，则可用该函数为请求创建 socket 或流。这可以避免只是为了重写默认的 `createConnection` 而创建自定义的 `Agent`。详见 [`agent.createConnection()`]。
  * `timeout` {number}: socket 超时的毫秒数。
  * `setHost` {boolean}: 是否自动添加 `Host` 请求头。默认为 `true`。
* `callback` {Function}
* 返回: {http.ClientRequest}

发送 HTTP 请求。

如果 `url` 是一个字符串，则自动使用 [`url.parse()`] 解析。
如果 `url` 是一个 [`URL`], 则自动转换成 `options` 选项。

如果同时指定了 `url` 和 `options`，则合并两个对象，其中 `options` 优先。

`callback` 会作为单次监听器添加到 [`'response'`] 事件。

返回的 `ClientRequest` 是可写流。
如果要通过 POST 请求上传文件，则写入到 `ClientRequest`。

```js
const postData = querystring.stringify({
  'msg': 'Node.js中文网'
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

// 将数据写入到请求主体。
req.write(postData);
req.end();
```

使用 `http.request()` 必须调用 `req.end()` 表明请求的结束，即使没有写入数据到请求主体。

如果请求过程中发生错误（DNS 解析错误、TCP 级的错误、或 HTTP 解析错误），则返回的请求对象会触发 `'error'` 事件。
如果 `'error'` 事件没有注册监听器，则抛出错误。

以下是需要注意的几个特殊的请求头。

* 发送 `'Connection: keep-alive'` 则服务器会保持连接直到下一次请求。

* 发送 `'Content-Length'` 会禁用默认的块编码。

* 发送 `'Expect'` 会立即发送请求头。通常情况下，当发送 `'Expect: 100-continue'` 时，需要设置超时时间和 `continue` 事件的监听器。

* 发送 `Authorization` 会代替 `auth` 计算基本身份验证。

例子，使用 [`URL`] 作为 `options`：

```js
const options = new URL('http://abc:xyz@example.com');

const req = http.request(options, (res) => {
  // ...
});
```

如果请求成功，则依次触发以下事件：

* `'socket'` 事件。
* `'response'` 事件。
  * 多次触发 `res` 的 `'data'` 事件（如果响应主体为空，则不会触发 `'data'` 事件，比如重定向）。
  * `res` 的 `'end'` 事件。
* `'close'` 事件。

如果连接出错，则依次触发以下事件：

* `'socket'` 事件。
* `'error'` 事件。
* `'close'` 事件。

如果连接成功之前调用 `req.abort()`，则依次触发以下事件：

* `'socket'` 事件。
* (此时调用 `req.abort()`)
* `'abort'` 事件。
* `'close'` 事件。
* `'error'` 事件并带上错误信息 `'Error: socket hang up'` 和错误码 `'ECONNRESET'`。

如果接收到响应之后调用 `req.abort()`，则依次触发以下事件：

* `'socket'` 事件。
* `'response'` 事件。
  * 多次触发 `res` 的 `'data'` 事件。
* (此时调用 `req.abort()`)
* `'abort'` 事件。
* `'close'` 事件。
  * `res` 的 `'aborted'` 事件。
  * `res` 的 `'end'` 事件。
  * `res` 的 `'close'` 事件。


