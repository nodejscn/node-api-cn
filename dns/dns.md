
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`dns` 模块包含属于两个不同类别的函数：

1) 使用底层操作系统工具执行名称解析但不一定执行任何网络通信的函数。 
此类别仅包含一个函数：[`dns.lookup()`]。 
希望以与同一操作系统上的其他应用程序相同的方式执行名称解析的开发者应使用 [`dns.lookup()`]。

示例，查找 `iana.org`：

```js
const dns = require('dns');

dns.lookup('iana.org', (err, address, family) => {
  console.log('地址: %j 地址族: IPv%s', address, family);
});
// 地址: "192.0.43.8" 地址族: IPv4
```

2) 连接到实际 DNS 服务器以执行名称解析并始终使用网络执行 DNS 查询的函数。 
此类别包含 `dns` 模块中除 [`dns.lookup()`] 之外的所有函数。 
这些函数不使用与 [`dns.lookup()`] 使用的同一组配置文件（例如 `/etc/hosts`）。 
这些函数应该由不希望使用底层操作系统的工具进行名称解析、而希望始终执行 DNS 查询的开发者使用，。

示例，解析 `'archive.org'` 然后逆向解析返回的 IP 地址：

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
      console.log(`地址 ${a} 逆向解析到域名: ${JSON.stringify(hostnames)}`);
    });
  });
});
```

两类函数有微妙的差别，详见[实现的注意事项][Implementation considerations section]。


