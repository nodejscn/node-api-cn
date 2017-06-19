
> 稳定性: 2 - 稳定的

`dns` 模块包含两类函数：

1) 第一类函数，使用底层操作系统工具进行域名解析，且无需进行网络通信。
这类函数只有一个：[`dns.lookup()`]。

例子，查找 `iana.org`：

```js
const dns = require('dns');

dns.lookup('iana.org', (err, address, family) => {
  console.log('IP 地址: %j 地址族: IPv%s', address, family);
});
// IP 地址: "192.0.43.8" 地址族: IPv4
```

2) 第二类函数，连接到一个真实的 DNS 服务器进行域名解析，且始终使用网络进行 DNS 查询。
这类函数包含了 `dns` 模块中除 [`dns.lookup()`] 以外的所有函数。
这些函数使用与 `dns.lookup()` 不同的配置文件（例如 `/etc/hosts`）。
这类函数适合于那些不想使用底层操作系统工具进行域名解析、而是想使用网络进行 DNS 查询的开发者。

例子，解析 `'archive.org'` 然后逆向解析返回的 IP 地址：

```js
const dns = require('dns');

dns.resolve4('archive.org', (err, addresses) => {
  if (err) throw err;

  console.log(`IP 地址: ${JSON.stringify(addresses)}`);

  addresses.forEach((a) => {
    dns.reverse(a, (err, hostnames) => {
      if (err) {
        throw err;
      }
      console.log(`IP 地址 ${a} 逆向解析到域名: ${JSON.stringify(hostnames)}`);
    });
  });
});
```

两类函数有微妙的差别，详见 [实现上的注意事项]。


