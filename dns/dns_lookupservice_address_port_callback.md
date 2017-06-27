<!-- YAML
added: v0.11.14
-->
- `address` {string}
- `port` {number}
- `callback` {Function}
  - `err` {Error}
  - `hostname` {string} e.g. `example.com`
  - `service` {string} e.g. `http`

将参数`address`和`port`传入操作系统底层`getnameinfo`服务来解析处理并返回主机名。

如果`address`不是有效的IP地址，会抛出`TypeError`。`port`必须是一个整数.如果不是规定的端口号，会抛出`TypeError`.

出错情况下，`err`是一个`Error`对象，`err.code`代码错误码。

```js
const dns = require('dns');
dns.lookupService('127.0.0.1', 22, (err, hostname, service) => {
  console.log(hostname, service);
  // Prints: localhost ssh
});
```

如果以 [`util.promisify()`][http://nodejs.cn/api/util.html#util_util_promisify_original] 方式进行调用, 它将返回一个包含`hostname`和`service`属性的Promise 对象。

