
> 稳定性: 2 - 稳定的

`dns`模块包含两个类型的函数：

1) 使用底层操作系统工具进行域名解析的函数，并不须要进行网络通信。这类函数只有一个：[`dns.lookup()`][]。** 如果希望在相同系统中与其他应用程序执行域名解析的行为一致，请使用[`dns.lookup()`][]函数 **

例如，查找`iana.org`

```js
const dns = require('dns');

dns.lookup('nodejs.org', (err, addresses, family) => {
  console.log('addresses:', addresses);
});
// address: "192.0.43.8" family: IPv4
```

2) 连接到实际DNS服务器进行域名解析的函数，并且始终使用网络执行DNS查询。这类函数包含除[`dns.lookup()`][]以外的所有`dns`模块中的函数。这类函数并未使用与[`dns.lookup()`][]相同的配置文件(例如： `/etc/hosts`)。 这类函数适合于那些不想使用底层操作系统工具进行域名解析，而是想使用网络执行DNS查询的开发者。

下面有一个解析`'archive.org'`的示例，然后反向解析返回的IP地址。

```js
const dns = require('dns');

dns.resolve4('archive.org', (err, addresses) => {
  if (err) throw err;

  console.log(`addresses: ${JSON.stringify(addresses)}`);

  addresses.forEach((a) => {
    dns.reverse(a, (err, hostnames) => {
      if (err) {
        throw err;
      }
      console.log(`reverse for ${a}: ${JSON.stringify(hostnames)}`);
    });
  });
});
```

两者之间的选择会产生微妙的结果，更多信息请查询[Implementation considerations section][]章节。


