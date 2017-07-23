<!-- YAML
added: v0.11.3
-->
- `servers` {string[]} array of [rfc5952][] formatted addresses

Sets the IP address and port of servers to be used when performing DNS
resolution. The `servers` argument is an array of [rfc5952][] formatted
addresses. If the port is the IANA default DNS port (53) it can be omitted.

For example:

```js
dns.setServers([
  '4.4.4.4',
  '[2001:4860:4860::8888]',
  '4.4.4.4:1053',
  '[2001:4860:4860::8888]:1053'
]);
```

`ip`地址无效将会报错。

`dns.setServers()`方法不要在DNS查询过程中使用。

