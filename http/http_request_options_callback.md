<!-- YAML
added: v0.3.6
-->

* `options` {Object}
  * `protocol` {String} 使用的协议。默认为 `'http:'`。
  * `host` {String} 请求发送至的服务器的域名或 IP 地址。默认为 `'localhost'`。
  * `hostname` {String} `host` 的别名。为了支持 [`url.parse()`]，`hostname` 优于 `host`。
  * `family` {Number} 当解析 `host` 和 `hostname` 时使用的 IP 地址族。
    有效值是 `4` 或 `6`。当未指定时，则同时使用 IP v4 和 v6。
  * `port` {Number} 远程服务器的端口。默认为 `80`。
  * `localAddress` {String} 要绑定到网络连接的本地接口。
  * `socketPath` {String} Unix 域 Socket（使用 host:port 或 socketPath 的其中之一）。
  * `method` {String} 一个指定 HTTP 请求方法的字符串。默认为 `'GET'`。
  * `path` {String} 请求的路径。默认为 `'/'`。
    应包括查询字符串（如有的话）。如 `'/index.html?page=12'`。
    当请求的路径中包含非法字符时，会抛出异常。
    目前只有空字符会被拒绝，但未来可能会变化。
  * `headers` {Object} 一个包含请求头的对象。
  * `auth` {String} 基本身份验证，如 `'user:password'` 来计算 Authorization 头。
  * `agent` {http.Agent|Boolean} 控制 [`Agent`] 的行为。
    可能的值有：
   * `undefined` (默认): 对该主机和端口使用 [`http.globalAgent`]。
   * `Agent` 对象：显式地使用传入的 `Agent`。
   * `false`: 产生一个新的使用默认值的 `Agent`。
  * `createConnection` {Function} 当不使用 `agent` 选项时，产生一个用于请求的 socket/stream 的函数。
    这可以用于避免创建一个自定义的 `Agent` 类，只是为了覆盖默认的 `createConnection` 函数。详见 [`agent.createConnection()`]。
  * `timeout` {Integer}: 一个数值，指定 socket 超时的毫秒数。
    它会在 socket 被连接时设置超时。
* `callback` {Function}
* 返回: {http.ClientRequest}

Node.js 维护每台服务器的多个连接来进行 HTTP 请求。
该函数允许显式地发出请求。

`options` 可以是一个对象或一个字符串。
如果 `options` 是一个字符串，它会被自动使用 [`url.parse()`] 解析。

可选的 `callback` 参数会被添加为 [`'response'`] 事件的单次监听器。

`http.request()` 返回一个 [`http.ClientRequest`] 类的实例。
`ClientRequest` 实例是一个可写流。
如果需要通过 POST 请求上传一个文件，则写入到 `ClientRequest` 对象。

例子：

```js
var postData = querystring.stringify({
  'msg' : 'Hello World!'
});

var options = {
  hostname: 'www.google.com',
  port: 80,
  path: '/upload',
  method: 'POST',
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Content-Length': Buffer.byteLength(postData)
  }
};

var req = http.request(options, (res) => {
  console.log(`STATUS: ${res.statusCode}`);
  console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
  res.setEncoding('utf8');
  res.on('data', (chunk) => {
    console.log(`主体: ${chunk}`);
  });
  res.on('end', () => {
    console.log('响应中已无数据。');
  });
});

req.on('error', (e) => {
  console.log(`请求遇到问题: ${e.message}`);
});

// 写入数据到请求主体
req.write(postData);
req.end();
```

注意，在例子中调用了 `req.end()`。
使用 `http.request()` 必须总是调用 `req.end()` 来表明请求已经结束，即使没有数据被写入请求主体。

如果请求过程中遇到任何错误（DNS 解析错误、TCP 级的错误、或实际的 HTTP 解析错误），则在返回的请求对象中会触发 `'error'` 事件。
对于所有的 `'error'` 事件，如果没有注册监听器，则抛出错误。

以下是需要注意的几个特殊的请求头。

* 发送一个 `'Connection: keep-alive'` 会通知 Node.js，服务器的连接应一直持续到下一个请求。

* 发送一个 `'Content-Length'` 请求头会禁用默认的块编码。

* 发送一个 `'Expect'` 请求头会立即发送请求头。
  通常情况下，当发送 `'Expect: 100-continue'` 时，应该设置一个超时并监听 `'continue'` 事件。
  详见 RFC2616 章节 8.2.3。

* 发送一个 Authorization 请求头会覆盖使用 `auth` 选项计算基本身份验证。

