<!-- YAML
added: v10.6.0
-->

* `hostname` {string}
* `options` {integer | Object}
  * `family` {integer} 地址类型必须是`4`, `6`, or `0`。其中，
  `0`代表同时返回了IPv4和IPv6地址。默认值是`0`。
  * `hints` {number} 传递一个或者多个支持的 `getaddrinfo`类型标志。多个类型记录可以或运算符连接起来。
  * `all` {boolean} 当值为`true`的时候, `Promise`会承诺解决数组里面的全部IP地址。
  否则的话，仅仅解决单一地址。默认值是`false`。
  * `verbatim` {boolean} 当值为`true`的时候, `Promise`的API使用DNS解析器根据他们返回的顺序使用IPv4和IPv6地址进行解析。
  如果为false，则将IPv4地址放在IPv6地址之前进行解析。 默认值：`false`（地址已重新排序），
  但预计在不久的将来会改变。新代码应使用`{ verbatim: true }`。 
  
  把一个主机名（例如'nodejs.org'）解析为第一个找到的A（IPv4）或AAAA（IPv6）IP地址。
  所有`option`属性都是可选的。如果`options`为整型，则值必须为`4`或`6` 
  - 如果`options`未提供，则返回能够找到的IPv4和IPv6地址。
  
当`all`选项设置为`true`时，将使用地址为具有属性`address`和`family`属性的对象数组来解析`Promise`。

发生错误时，`Promise`会被[`Error`][]对象拒绝，其中“ err.code”是错误代码，
请注意一点，`err.code`的值，不仅仅在主机名不存在时，同时在查找以其他方式
（例如，没有可用的文件描述符）失败时，`err.code`都将被设置为 `'ENOTFOUND'`。

[`dnsPromises.lookup()`][] 不一定与DNS协议有关。该实现使用操作系统工具，该工具可以将名称与地址相关联，反之亦然。
 这种操作实现会对任何Node.js程序的行为产生微妙重要的后果。
 因此，在使用`dnsPromises.lookup()`之前，请花一些时间查看注意事项[Implementation considerations section][]。


Example usage:

```js
const dns = require('dns');
const dnsPromises = dns.promises;
const options = {
  family: 6,
  hints: dns.ADDRCONFIG | dns.V4MAPPED,
};

dnsPromises.lookup('example.com', options).then((result) => {
  console.log('address: %j family: IPv%s', result.address, result.family);
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
});

// 当options.all为true时，结果将为数组。
options.all = true;
dnsPromises.lookup('example.com', options).then((result) => {
  console.log('addresses: %j', result);
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
});
```

