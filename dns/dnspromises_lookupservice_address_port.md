<!-- YAML
added: v10.6.0
-->

* `address` {string}
* `port` {number}

使用操作系统底层的`getnameinfo`实现去解析`address` and `port`得到主机名和服务。

如果`address`不是有效的IP地址，则将引发`TypeError`。 该`端口`必须为一个数字。 如果不是合法端口，则将引发`TypeError`。

发生错误时，`Promise`将被[`Error`][]对象拒绝，其中`err.code`是错误代码。



```js
const dnsPromises = require('dns').promises;
dnsPromises.lookupService('127.0.0.1', 22).then((result) => {
  console.log(result.hostname, result.service);
  // Prints: localhost ssh
});
```

