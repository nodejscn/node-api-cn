<!-- YAML
added: v0.1.27
-->
- `hostname` {string} Hostname to resolve.
- `rrtype` {string} Resource record type. Default: `'A'`.
- `callback` {Function}
  - `err` {Error}
  - `records` {string[] | Object[] | Object}

Uses the DNS protocol to resolve a hostname (e.g. `'nodejs.org'`) into an array
of the resource records. The `callback` function has arguments
`(err, records)`. When successful, `records` will be an array of resource
records. The type and structure of individual results varies based on `rrtype`:

|  `rrtype` | `records` contains             | Result type | Shorthand method         |
|-----------|--------------------------------|-------------|--------------------------|
| `'A'`     | IPv4 addresses (default)       | {string}    | [`dns.resolve4()`][]     |
| `'AAAA'`  | IPv6 addresses                 | {string}    | [`dns.resolve6()`][]     |
| `'CNAME'` | canonical name records         | {string}    | [`dns.resolveCname()`][] |
| `'MX'`    | mail exchange records          | {Object}    | [`dns.resolveMx()`][]    |
| `'NAPTR'` | name authority pointer records | {Object}    | [`dns.resolveNaptr()`][] |
| `'NS'`    | name server records            | {string}    | [`dns.resolveNs()`][]    |
| `'PTR'`   | pointer records                | {string}    | [`dns.resolvePtr()`][]   |
| `'SOA'`   | start of authority records     | {Object}    | [`dns.resolveSoa()`][]   |
| `'SRV'`   | service records                | {Object}    | [`dns.resolveSrv()`][]   |
| `'TXT'`   | text records                   | {string}    | [`dns.resolveTxt()`][]   |
| `'ANY'`   | any records                    | {Object}    | [`dns.resolveAny()`][]   |

On error, `err` is an [`Error`][] object, where `err.code` is one of the
[DNS error codes](#dns_error_codes).

