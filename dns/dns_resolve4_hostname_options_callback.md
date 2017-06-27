<!-- YAML
added: v0.1.16
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9296
    description: This method now supports passing `options`,
                 specifically `options.ttl`.
-->
- `hostname` {string} Hostname to resolve.
- `options` {Object}
  - `ttl` {boolean} Retrieve the Time-To-Live value (TTL) of each record.
    When `true`, the callback receives an array of
    `{ address: '1.2.3.4', ttl: 60 }` objects rather than an array of strings,
    with the TTL expressed in seconds.
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[] | Object[]}

使用`DNS`协议解析IPv4地址主机名(`A`记录)。`adresses`参数是传递给`callback`函数的IPv4地址数组。（例如：`['74.125.79.104', '74.125.79.105', '74.125.79.106']`）


