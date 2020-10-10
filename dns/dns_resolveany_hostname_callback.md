
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `ret` {Object[]}

使用 DNS 协议解析所有记录（也称为 `ANY` 或 `*` 查询）。 
传给 `callback` 函数的 `ret` 参数将会是一个包含各种类型记录的数组。 
每个对象都有一个 `callback` 属性，表明当前记录的类型。 
根据 `type`，对象上将会显示其他属性：

| 类型 | 属性 |
|------|------------|
| `'A'` | `address`/`ttl` |
| `'AAAA'` | `address`/`ttl` |
| `'CNAME'` | `value` |
| `'MX'` | 指向 [`dns.resolveMx()`][] |
| `'NAPTR'` | 指向 [`dns.resolveNaptr()`][] |
| `'NS'` | `value` |
| `'PTR'` | `value` |
| `'SOA'` | 指向 [`dns.resolveSoa()`][] |
| `'SRV'` | 指向 [`dns.resolveSrv()`][] |
| `'TXT'` | 这种类型的记录包含一个名为 `entries` 的数组属性，它指向 [`dns.resolveTxt()`]，例如：`{ entries: ['...'], type: 'TXT' }` |

以下是传给回调的 `ret` 对象的示例：

<!-- eslint-disable semi -->
```js
[ { type: 'A', address: '127.0.0.1', ttl: 299 },
  { type: 'CNAME', value: 'example.com' },
  { type: 'MX', exchange: 'alt4.aspmx.l.example.com', priority: 50 },
  { type: 'NS', value: 'ns1.example.com' },
  { type: 'TXT', entries: [ 'v=spf1 include:_spf.example.com ~all' ] },
  { type: 'SOA',
    nsname: 'ns1.example.com',
    hostmaster: 'admin.example.com',
    serial: 156696742,
    refresh: 900,
    retry: 900,
    expire: 1800,
    minttl: 60 } ]
```

DNS 服务器运营商可以选择不响应 `ANY` 查询。 
调用 [`dns.resolve4()`]、[`dns.resolveMx()`] 等单个方法可能更好。 
有关更多详细信息，请参见 [RFC 8482]。

