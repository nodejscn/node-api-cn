<!-- YAML
added: v0.1.27
-->
* `hostname` {string} 解析的主机名。
* `rrtype` {string} 资源记录类型。**默认值:** `'A'`。
* `callback` {Function}
  - `err` {Error}
  - `records` {string[] | Object[] | Object}

使用 DNS 协议将主机名（例如 `'nodejs.cn'`）解析为一个资源记录的数组。
`callback` 函数的参数为 `(err, records)`。
当成功时，`records` 将会是一个资源记录的数组。
它的类型和结构取决于 `rrtype`：

|  `rrtype` | `records` 包含             | 结果的类型 | 快捷方法         |
|-----------|--------------------------------|-------------|--------------------------|
| `'A'`     | IPv4 地址 (默认)       | {string}    | [`dns.resolve4()`][]     |
| `'AAAA'`  | IPv6 地址                 | {string}    | [`dns.resolve6()`][]     |
| `'ANY'`   | 任何记录                   | {Object}    | [`dns.resolveAny()`][]   |
| `'CNAME'` | 规范名称记录         | {string}    | [`dns.resolveCname()`][] |
| `'MX'`    | 邮件交换记录          | {Object}    | [`dns.resolveMx()`][]    |
| `'NAPTR'` | 名称权限指针记录 | {Object}    | [`dns.resolveNaptr()`][] |
| `'NS'`    | 名称服务器记录            | {string}    | [`dns.resolveNs()`][]    |
| `'PTR'`   | 指针记录               | {string}    | [`dns.resolvePtr()`][]   |
| `'SOA'`   | 开始授权记录     | {Object}    | [`dns.resolveSoa()`][]   |
| `'SRV'`   | 服务记录                | {Object}    | [`dns.resolveSrv()`][]   |
| `'TXT'`   | 文本记录                   | {string[]}  | [`dns.resolveTxt()`][]   |

当出错时，`err` 是一个 [`Error`] 对象，其中 `err.code` 是 [DNS 错误码][_dns_error_codes]的一种。
