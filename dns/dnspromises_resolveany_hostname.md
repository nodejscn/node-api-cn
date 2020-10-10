<!-- YAML
added: v10.6.0
-->

* `hostname` {string}

Uses the DNS protocol to resolve all records (also known as `ANY` or `*` query).
On success, the `Promise` is resolved with an array containing various types of
records. Each object has a property `type` that indicates the type of the
current record. And depending on the `type`, additional properties will be
present on the object:

| Type | Properties |
|------|------------|
| `'A'` | `address`/`ttl` |
| `'AAAA'` | `address`/`ttl` |
| `'CNAME'` | `value` |
| `'MX'` | Refer to [`dnsPromises.resolveMx()`][] |
| `'NAPTR'` | Refer to [`dnsPromises.resolveNaptr()`][] |
| `'NS'` | `value` |
| `'PTR'` | `value` |
| `'SOA'` | Refer to [`dnsPromises.resolveSoa()`][] |
| `'SRV'` | Refer to [`dnsPromises.resolveSrv()`][] |
| `'TXT'` | This type of record contains an array property called `entries` which refers to [`dnsPromises.resolveTxt()`][], e.g. `{ entries: ['...'], type: 'TXT' }` |

Here is an example of the result object:

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

