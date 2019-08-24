<!-- YAML
added: v0.11.14
-->
* `address` {string}
* `port` {number}
* `callback` {Function}
  - `err` {Error}
  - `hostname` {string} 例如 `nodejs.cn`。
  - `service` {string} 例如 `http`。

使用操作系统的底层 `getnameinfo` 实现将给定的 `address` 和 `port` 解析为主机名和服务。

如果 `address` 不是有效的 IP 地址，则将会抛出 `TypeError`。
`port` 会被强制转换为数字。
如果它不是合法的端口，则抛出 `TypeError`。

出错情况下，`err` 是一个 [`Error`] 对象，其中 `err.code` 是错误码。

```js
const dns = require('dns');
dns.lookupService('127.0.0.1', 22, (err, hostname, service) => {
  console.log(hostname, service);
  // 打印: localhost ssh
});
```

如果调用此方法的 [`util.promisify()`] 化的版本，则它返回的 `Promise` 会返回一个具有 `hostname` 和 `service` 属性的 `Object`。

