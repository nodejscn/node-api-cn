<!-- YAML
added: v0.1.90
changes:
  - version: v1.2.0
    pr-url: https://github.com/nodejs/node/pull/744
    description: The `all` option is supported now.
-->
- `hostname` {string}
- `options` {integer | Object}
  - `family` {integer} The record family. Must be `4` or `6`. IPv4
    and IPv6 addresses are both returned by default.
  - `hints` {number} One or more [supported `getaddrinfo` flags][]. Multiple
    flags may be passed by bitwise `OR`ing their values.
  - `all` {boolean} When `true`, the callback returns all resolved addresses in
    an array. Otherwise, returns a single address. Defaults to `false`.
- `callback` {Function}
  - `err` {Error}
  - `address` {string} A string representation of an IPv4 or IPv6 address.
  - `family` {integer} `4` or `6`, denoting the family of `address`.

解析`hostname`(例如：`'nodejs.org'`)为第一个找到的A（IPv4）或AAAA（IPv6）记录。`options`可以是对象或者整数。如果`options`没有被提供，那么IPv4 和 IPv6都是有效的。如果`options`是整数，只能是`4`或`6`。

另外，`options`可以是一个含有以下属性的对象：
* `family` {Number} - T地址族。如果提供，必须为整数4或6。如果没有提供，只接受IPv4和IPv6地址。
* `hints`: {Number} - 如果提供，它必须是一个或多个支持的`getaddrinfo`标识。如果没有提供，那么没有标识被传递给`getaddrinfo`。多个标识可以通过在逻辑上`OR`ing它们的值，来传递给hints。支持的`getaddrinfo`标识请参阅下文。有关支持的标志的更多信息请查询[supported `getaddrinfo` flags][]章节。
* `all`: {Boolean} - 值为`true`时， 回调函数返回一个包含所有解析后地址的数组，否则只返回一个地址。默认值为`false`。

所有的参数都是可选的。

回调函数包含`(err, address, family)`参数。`address`是IPv4或IPv6地址字符串。`family`、是整数4或6，表示地址族（不一定是最初传递给查找的值）。

当`all`属性被设置为`true`时，回调函数参数变为`(err, addresses)`，`addresses`则变成一个由`address` 和 `family` 属性组成的对象数组。

发生错误时，`err`是一个[`Error`][]对象，`err.code`是错误码。不仅在主机名不存在时，在如没有可用的文件描述符等情况下查找失败，err.code也会被设置为`'ENOENT'`。

`dns.lookup()` 不需要与DNS协议有任何关系。它仅仅是一个连接名字和地址的操作系统功能。在任何的node.js程序中，它的实现对表现有一些微妙但是重要的影响。在使用`dns.lookup()`之前请花些时间查询[Implementation considerations section][]章节。

使用例子：

```js
const dns = require('dns');
const options = {
  family: 6,
  hints: dns.ADDRCONFIG | dns.V4MAPPED,
};
dns.lookup('example.com', options, (err, address, family) =>
  console.log('address: %j family: IPv%s', address, family));
// address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

// When options.all is true, the result will be an Array.
options.all = true;
dns.lookup('example.com', options, (err, addresses) =>
  console.log('addresses: %j', addresses));
// addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
```

If this method is invoked as its [`util.promisify()`][]ed version, and `all`
is not set to `true`, it returns a Promise for an object with `address` and
`family` properties.

