<!-- YAML
added: v0.1.16
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9296
    description: This method now supports passing `options`,
                 specifically `options.ttl`.
-->
* `hostname` {string} 需要解析的主机名。
* `options` {Object}
  - `ttl` {boolean} 记录每一条记录的存活次数 (TTL)。当为 `true` 时，回调会接收一个带有 TTL 秒数记录的类似 `{ address: '1.2.3.4', ttl: 60 }` 对象的数组，而不是字符串的数组。
* `callback` {Function}
  - `err` {Error}
  - `addresses` {string[] | Object[]}

使用 DNS 协议为 `hostname` 解析 IPv4 地址（`A` 记录）。
`adresses` 参数是传给 `callback` 函数的 IPv4 地址数组（例如：`['74.125.79.104', '74.125.79.105', '74.125.79.106']`）。


