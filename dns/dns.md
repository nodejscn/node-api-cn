
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

<!-- source_link=lib/dns.js -->

`dns` 模块用于启用名称解析。 
例如，使用它来查找主机名的 IP 地址。

尽管以[域名系统（DNS）][Domain Name System (DNS)]命名，但它并不总是使用 DNS 协议进行查找。 
[`dns.lookup()`] 使用操作系统功能来执行名称解析。 
它可能不需要执行任何网络通信。 
若要像同一系统上其他应用程序一样执行名称解析，则使用 [`dns.lookup()`]。

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
使用这些函数可以始终执行 DNS 查询（绕过其他的名称解析功能）。

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

有关更多信息，参见[实现的注意事项][Implementation considerations section]。


