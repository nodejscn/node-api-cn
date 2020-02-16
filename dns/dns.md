
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`dns` 模块用于启用名称解析。 
例如，使用它来查找主机名的 IP 地址。

尽管以域名系统（DNS）命名，但它并不总是使用 DNS 协议进行查找。 
[`dns.lookup()`] 使用操作系统功能来执行名称解析。 
它可能不需要执行任何网络通信。 
希望以与同一操作系统上其他应用程序相同的方式执行名称解析的开发者应使用 [`dns.lookup()`]。

```js
const dns = require('dns');

dns.lookup('example.org', (err, address, family) => {
console.log('地址: %j 地址族: IPv%s', address, family);
});
// 地址: "93.184.216.34" 地址族: IPv4
```

`dns` 模块中的所有其他函数都连接到实际的 DNS 服务器以执行名称解析。 
它们将会始终使用网络执行 DNS 查询。 
这些函数不使用与 [`dns.lookup()`] 使用的同一组配置文件（例如 `/etc/hosts`）。 
这些函数应由不想使用底层操作系统的功能进行名称解析、而希望始终执行 DNS 查询的开发者使用。

```js
const dns = require('dns');

dns.resolve4('archive.org', (err, addresses) => {
  if (err) throw err;

  console.log(`地址: ${JSON.stringify(addresses)}`);

  addresses.forEach((a) => {
    dns.reverse(a, (err, hostnames) => {
      if (err) {
        throw err;
      }
      console.log(`地址 ${a} 逆向到: ${JSON.stringify(hostnames)}`);
    });
  });
});
```

有关更多信息，参阅[实现的注意事项][Implementation considerations section]。


