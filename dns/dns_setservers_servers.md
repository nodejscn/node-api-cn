<!-- YAML
added: v0.11.3
-->
- `servers` {string[]}

设置解析时使用的服务器IP地址。`servers`服务器参数是一个IPv4或IPv6地址的数组.

如果指定的ip包含端口，端口会被移除。

`ip`地址无效将会报错。

`dns.setServers()`方法不要在DNS查询过程中使用。

