<!-- YAML
added: v0.1.16
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9296
    description: This method now supports passing `options`,
                 specifically `options.ttl`.
-->
- `hostname` {string} 需要解析的主机名。
- `options` {Object}
  - `ttl` {boolean} 记录每一条记录的存活次数 (TTL)。如果为 `true`， 返回的结果将会为 `Object` 的数组，就像 `{ address: '1.2.3.4', ttl: 60 }` 带有 `TTL` 秒数的记录，而不是 `string` 的数组.
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[] | Object[]}

使用`DNS`协议解析IPv4地址主机名(`A`记录)。`adresses`参数是传递给`callback`函数的IPv4地址数组。（例如：`['74.125.79.104', '74.125.79.105', '74.125.79.106']`）


