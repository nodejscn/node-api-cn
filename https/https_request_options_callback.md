<!-- YAML
added: v0.3.6
-->

向一个安全的服务器发起一个请求.

参数`options` 可以是一个对象或是一个字符串. 如果参数`options` 是一个字符串, 它自动被[`url.parse()`][]所解析.


所有来自 [`http.request()`][] 的参数是有效的.

例子:

```js
const https = require('https');

var options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET'
};

var req = https.request(options, (res) => {
  console.log('statusCode:', res.statusCode);
  console.log('headers:', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });
});

req.on('error', (e) => {
  console.error(e);
});
req.end();
```

`options`参数可以有以下选择：

- `host`: 一个处理请求的服务器的域名或者IP地址，默认是`loaclhost`.
- `hostname`: `host`的别名. 为了更好地支持`url.parse()`， `hostname` 比`host`更被推荐使用.
- `family`: 用于解析`host` and `hostname`的IP地址族.
  `4` 或者 `6` 都是有效数值. 当不被指定时，IPv4 和 IPv6都将被使用
- `port`: 远程服务器的端口. 默认是443.
- `localAddress`: 绑定用来连接的本地接口.
- `socketPath`: Unix域套接字（用一个 host:port 或者socketPath）.
- `method`: 一个用来确定HTTP请求方法的字符串. 默认是`'GET'`.
- `path`: 请求路径. 默认是`'/'`. 如果有的话，应该包含请求字符串。
  例如. `'/index.html?page=12'`. 当请求路径包含非法字符的时候，将抛出异常。 目前, 只有空格字符被拒绝，但是未来可能会有改变.
- `headers`: 一个包含请求头的对象.
- `auth`: 基本认证， 例如 `'user:password'` 来计算认证头.
- `agent`: 控制 [`Agent`][] 的行为. 当用代理时，请求默认是`Connection: keep-alive`. 可能的值:
 - `undefined` (默认): 这个主机和端口用[`globalAgent`][].
 - `Agent` 对象: 显示地在`Agent`中用传进来的参数.
 - `false`: opts out of connection pooling with an Agent, 默认是
   `Connection: close`.

下面是来自[`tls.connect()`][]的参数，它也可以被设置为:

- `pfx`: 证书, 用于SSL的私钥和 CA 证书. 默认是 `null`.
- `key`: 用于SSL的私钥. 默认是 `null`.
- `passphrase`: 用于私钥或是pfx的密码字符串. 默认是 `null`.
- `cert`: 公共x509证书. 默认是 `null`.
- `ca`: 一个字符串, [`缓存`][] 或 字符串数组 或 PEM格式的可信赖证书的[`缓存`][]。 如果这被忽略，那么著名的根证书将被使用，比如说VeriSign数字证书. 这些被用来授权连接.
- `ciphers`: 一个用来描述要使用或排除的密码的字符串. 查看
  <https://www.openssl.org/docs/man1.0.2/apps/ciphers.html#CIPHER-LIST-FORMAT> 获取格式的细节.
- `rejectUnauthorized`: 如果设置为`true`, 服务器证书根据CA提供的列表来进行验证。 如果验证失败的话，一个 `'error'` 事件将被触发. 验证发生在连接层次, *早于* HTTP请求的发送. 默认是 `true`.
- `secureProtocol`: 使用的SSL方法，例如， `SSLv3_method` 来强制使用
  SSL 版本３. 可能的只取决于安装的OpenSSL的版本，它被定义在[`SSL_METHODS`][]常数中.
- `servername`: SNI (Server Name Indication) TLS 扩展的服务器名.

为了确定这些参数, 用一个定制的 [`Agent`][].

例子:

```js
var options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET',
  key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
  cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem')
};
options.agent = new https.Agent(options);

var req = https.request(options, (res) => {
  ...
});
```

可能的话, opt out of connection pooling by not using an `Agent`.

例子:

```js
var options = {
  hostname: 'encrypted.google.com',
  port: 443,
  path: '/',
  method: 'GET',
  key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
  cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
  agent: false
};

var req = https.request(options, (res) => {
  ...
});
```

[`Agent`]: #https_class_https_agent
[`Buffer`]: buffer.html#buffer_buffer
[`globalAgent`]: #https_https_globalagent
[`http.Agent`]: http.html#http_class_http_agent
[`http.close()`]: http.html#http_server_close_callback
[`http.get()`]: http.html#http_http_get_options_callback
[`http.listen()`]: http.html#http_server_listen_port_hostname_backlog_callback
[`http.request()`]: http.html#http_http_request_options_callback
[`http.Server#setTimeout()`]: http.html#http_server_settimeout_msecs_callback
[`http.Server#timeout`]: http.html#http_server_timeout
[`http.Server`]: http.html#http_class_http_server
[`https.Agent`]: #https_class_https_agent
[`https.request()`]: #https_https_request_options_callback
[`SSL_METHODS`]: https://www.openssl.org/docs/man1.0.2/ssl/ssl.html#DEALING-WITH-PROTOCOL-METHODS
[`tls.connect()`]: tls.html#tls_tls_connect_options_callback
[`tls.createServer()`]: tls.html#tls_tls_createserver_options_secureconnectionlistener
[`url.parse()`]: url.html#url_url_parse_urlstring_parsequerystring_slashesdenotehost
