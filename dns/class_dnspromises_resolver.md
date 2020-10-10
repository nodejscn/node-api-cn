<!-- YAML
added: v10.6.0
-->

一个DNS请求的独立解析器。

创建新的解析器将使用默认服务器设置。使用[`resolver.setServers()`][`dnsPromises.setServers()`]设置解析器的服务器并不会影响其他的解析器：
```js
const { Resolver } = require('dns').promises;
const resolver = new Resolver();
resolver.setServers(['4.4.4.4']);

// 该请求使用4.4.4.4的服务器，独立于全局设置。
resolver.resolve4('example.org').then((addresses) => {
  // ...
});

// 或者, 你可以用`async-await`编写异步代码。
(async function() {
  const addresses = await resolver.resolve4('example.org');
})();
```

以下是`dns.Promises` API提供的方法。

* [`resolver.getServers()`][`dnsPromises.getServers()`]
* [`resolver.resolve()`][`dnsPromises.resolve()`]
* [`resolver.resolve4()`][`dnsPromises.resolve4()`]
* [`resolver.resolve6()`][`dnsPromises.resolve6()`]
* [`resolver.resolveAny()`][`dnsPromises.resolveAny()`]
* [`resolver.resolveCname()`][`dnsPromises.resolveCname()`]
* [`resolver.resolveMx()`][`dnsPromises.resolveMx()`]
* [`resolver.resolveNaptr()`][`dnsPromises.resolveNaptr()`]
* [`resolver.resolveNs()`][`dnsPromises.resolveNs()`]
* [`resolver.resolvePtr()`][`dnsPromises.resolvePtr()`]
* [`resolver.resolveSoa()`][`dnsPromises.resolveSoa()`]
* [`resolver.resolveSrv()`][`dnsPromises.resolveSrv()`]
* [`resolver.resolveTxt()`][`dnsPromises.resolveTxt()`]
* [`resolver.reverse()`][`dnsPromises.reverse()`]
* [`resolver.setServers()`][`dnsPromises.setServers()`]

