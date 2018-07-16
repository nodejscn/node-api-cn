<!-- YAML
added: v10.6.0
-->
- `hostname` {string} Hostname to resolve.
- `rrtype` {string} Resource record type. **Default:** `'A'`.

Uses the DNS protocol to resolve a hostname (e.g. `'nodejs.org'`) into an array
of the resource records. When successful, the `Promise` is resolved with an
array of resource records. The type and structure of individual results vary
based on `rrtype`:

|  `rrtype` | `records` contains             | Result type | Shorthand method         |
|-----------|--------------------------------|-------------|--------------------------|
| `'A'`     | IPv4 addresses (default)       | {string}    | [`dnsPromises.resolve4()`][]     |
| `'AAAA'`  | IPv6 addresses                 | {string}    | [`dnsPromises.resolve6()`][]     |
| `'ANY'`   | any records                    | {Object}    | [`dnsPromises.resolveAny()`][]   |
| `'CNAME'` | canonical name records         | {string}    | [`dnsPromises.resolveCname()`][] |
| `'MX'`    | mail exchange records          | {Object}    | [`dnsPromises.resolveMx()`][]    |
| `'NAPTR'` | name authority pointer records | {Object}    | [`dnsPromises.resolveNaptr()`][] |
| `'NS'`    | name server records            | {string}    | [`dnsPromises.resolveNs()`][]    |
| `'PTR'`   | pointer records                | {string}    | [`dnsPromises.resolvePtr()`][]   |
| `'SOA'`   | start of authority records     | {Object}    | [`dnsPromises.resolveSoa()`][]   |
| `'SRV'`   | service records                | {Object}    | [`dnsPromises.resolveSrv()`][]   |
| `'TXT'`   | text records                   | {string[]}  | [`dnsPromises.resolveTxt()`][]   |

On error, the `Promise` is rejected with an [`Error`][] object, where `err.code`
is one of the [DNS error codes](#dns_error_codes).

