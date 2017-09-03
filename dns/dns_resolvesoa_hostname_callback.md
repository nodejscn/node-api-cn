<!-- YAML
added: v0.11.10
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `address` {Object}

使用DNS协议处理主机名子域名记录(`SOA`记录)。`addresses`参数为一个对象包含以下属性：

* `nsname`
* `hostmaster`
* `serial`
* `refresh`
* `retry`
* `expire`
* `minttl`

<!-- eslint-skip -->
```js
{
  nsname: 'ns.example.com',
  hostmaster: 'root.example.com',
  serial: 2013101809,
  refresh: 10000,
  retry: 2400,
  expire: 604800,
  minttl: 3600
}
```

