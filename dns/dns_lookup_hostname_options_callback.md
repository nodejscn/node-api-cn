<!-- YAML
added: v0.1.90
changes:
  - version: v8.5.0
    pr-url: https://github.com/nodejs/node/pull/14731
    description: The `verbatim` option is supported now.
  - version: v1.2.0
    pr-url: https://github.com/nodejs/node/pull/744
    description: The `all` option is supported now.
-->
* `hostname` {string}
* `options` {integer | Object}
  - `family` {integer} 记录的地址族。必须为 `4`、`6` 或 `0`。`0` 值表示返回 IPv4 和 IPv6 地址。**默认值:** `0`。
  - `hints` {number} 一个或多个[受支持的 `getaddrinfo` 标志][supported `getaddrinfo` flags]。可以通过按位 `OR` 运算它们的值来传递多个标志。
  - `all` {boolean} 当为 `true`  时，则回调将会返回数组中所有已解析的地址。否则，返回单个地址。**默认值：** `false`。
  - `verbatim` {boolean} 当为 `true` 时，则回调按 DNS 解析器返回的顺序接收 IPv4 和 IPv6 地址。当为 `false` 时，则 IPv4 地址放在 IPv6 地址之前。
     **默认值:** 当前为 `false`（地址已重新排序）但预计在不久的将来会发生变化。新代码应使用 `{ verbatim: true }`。
* `callback` {Function}
  - `err` {Error}
  - `address` {string} IPv4 或 IPv6 地址的字符串表示形式。
  - `family` {integer} `4` 或 `6`，表示 `address` 的地址族，如果地址不是 IPv4 或 IPv6 地址，则为 `0`。`0` 可能是操作系统使用的名称解析服务中的错误的指示符。

解析主机名（例如：`'nodejs.cn'`）为第一个找到的 A（IPv4）或 AAAA（IPv6）记录。
所有的 `option` 属性都是可选的。
如果 `options` 是整数，则只能是 `4` 或 `6`。
如果 `options` 没有被提供，则 IPv4 和 IPv6 都是有效的。

当 `all` 选项被设置为 `true` 时，`callback` 的参数会变为 `(err, addresses)`，其中 `addresses` 变成一个由 `address` 和 `family` 属性组成的对象数组。

当发生错误时，`err` 是一个 [`Error`] 对象，其中 `err.code` 是错误码。
不仅在主机名不存在时，在如没有可用的文件描述符等情况下查找失败，`err.code` 也会被设置为 `'ENOTFOUND'`。

`dns.lookup()` 不需要与 DNS 协议有任何关系。
它仅仅是一个连接名字和地址的操作系统功能。
在任何的 Node.js 程序中，它的实现对表现有一些微妙但是重要的影响。
在使用 `dns.lookup()` 之前请花些时间查询[实现的注意事项][Implementation considerations section]章节。

使用示例：

```js
const dns = require('dns');
const options = {
  family: 6,
  hints: dns.ADDRCONFIG | dns.V4MAPPED,
};
dns.lookup('example.com', options, (err, address, family) =>
  console.log('地址: %j 地址族: IPv%s', address, family));
// 地址: "2606:2800:220:1:248:1893:25c8:1946" 地址族: IPv6

// 当 options.all 为 true 时，则结果将会是一个数组。
options.all = true;
dns.lookup('example.com', options, (err, addresses) =>
  console.log('地址: %j', addresses));
// 地址: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
```

如果调用此方法的 [`util.promisify()`] 化的版本，并且 `all` 未设置为 `true`，则它返回的 Promise 会返回一个具有 `address` 和 `family` 属性的对象。


