
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `ret` {Object[]}

Uses the DNS protocol to resolve all records (also known as `ANY` or `*` query).
The `ret` argument passed to the `callback` function will be an array containing
various types of records. Each object has a property `type` that indicates the
type of the current record. And depending on the `type`, additional properties
will be present on the object:

| Type | Properties |
|------|------------|
| `"A"` | `address` / `ttl` |
| `"AAAA"` | `address` / `ttl` |
| `"CNAME"` | `value` |
| `"MX"` | Refer to [`dns.resolveMx()`][] |
| `"NAPTR"` | Refer to [`dns.resolveNaptr()`][] |
| `"NS"` | `value` |
| `"PTR"` | `value` |
| `"SOA"` | Refer to [`dns.resolveSoa()`][] |
| `"SRV"` | Refer to [`dns.resolveSrv()`][] |
| `"TXT"` | This type of record contains an array property called `entries` which refers to [`dns.resolveTxt()`][], eg. `{ entries: ['...'], type: 'TXT' }` |

Here is a example of the `ret` object passed to the callback:

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

