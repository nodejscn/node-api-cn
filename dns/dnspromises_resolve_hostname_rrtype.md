<!-- YAML
added: v10.6.0
-->

* `hostname` {string} Host name to resolve.
* `rrtype` {string} Resource record type. **Default:** `'A'`.

使用DNS协议将主机名（例如“ nodejs.org”）解析为资源记录的数组。
成功后，将通过一系列资源记录来解决实现`Promise`。
各个结果的类型和结构根据`rrtype`的不同而有所不同：

|  `rrtype` | `records` contains             | Result type | Shorthand method         |
|-----------|--------------------------------|-------------|--------------------------|
| `'A'`     | IPv4 地址（默认）               | {string}    | [`dnsPromises.resolve4()`][]     |
| `'AAAA'`  | IPv6 地址                      | {string}    | [`dnsPromises.resolve6()`][]     |
| `'ANY'`   | 任何记录                        | {Object}    | [`dnsPromises.resolveAny()`][]   |
| `'CNAME'` | 规范名称记录                    | {string}    | [`dnsPromises.resolveCname()`][] |
| `'MX'`    | 将域名指向邮件服务器地址         | {Object}    | [`dnsPromises.resolveMx()`][]    |
| `'NAPTR'` | 名称权限指针记录                | {Object}    | [`dnsPromises.resolveNaptr()`][] |
| `'NS'`    | 将子域名指定其他DNS服务器解析    | {string}    | [`dnsPromises.resolveNs()`][]    |
| `'PTR'`   | 指针记录                       | {string}    | [`dnsPromises.resolvePtr()`][]   |
| `'SOA'`   | 权限记录的开始                  | {Object}    | [`dnsPromises.resolveSoa()`][]   |
| `'SRV'`   | 记录提供特定的服务的服务器       | {Object}    | [`dnsPromises.resolveSrv()`][]   |
| `'TXT'`   | 文本长度限制512，通常做SPF记录（反垃圾邮件）    | {string[]}  | [`dnsPromises.resolveTxt()`][]   |

如果出错，则`Promise`会被[`Error`][]对象拒绝，其中`err.code`是[DNS错误代码](#dns_error_codes)之一。
