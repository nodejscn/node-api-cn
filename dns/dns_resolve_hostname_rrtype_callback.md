<!-- YAML
added: v0.1.27
-->
- `hostname` {string} 解析的主机名。
- `rrtype` {string} 资源记录类型. 默认: `'A'`.
- `callback` {Function}
  - `err` {Error}
  - `records` {string[] | Object[] | Object}

使用DNS协议来解析一个主机名(e.g. `'nodejs.org'`)为一个资源记录的数组。回调函数的参数为`(err, records)`。当成功时，`records`将是一个资源记录的数组。它的类型和结构取决于`rrtype`：

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
| `'TXT'`   | text records                   | {string[]}  | [`dns.resolveTxt()`][]   |
| `'ANY'`   | any records                    | {Object}    | [`dns.resolveAny()`][]   |

出错时，`err`是一个[`Error`][] object，`err.code`是[DNS error codes](#dns_error_codes)的一种。
