<!-- YAML
added: v0.1.16
-->
- `ip` {string}
- `callback` {Function}
  - `err` {Error}
  - `hostnames` {string[]}

执行一个反向DNS查询返回IPv4或IPv6地址的主机名的数组。

出错情况下，`err`是一个`Error`对象，`err.code`代码错误码。错误码列表：[here](https://nodejs.org/dist/latest-v8.x/docs/api/dns.html#dns_error_codes).

