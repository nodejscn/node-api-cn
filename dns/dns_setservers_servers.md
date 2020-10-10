<!-- YAML
added: v0.11.3
-->
* `servers` {string[]} [RFC 5952] 格式的地址数组。

设置执行 DNS 解析时要使用的服务器的 IP 地址和端口。 
`servers` 参数是 [RFC 5952] 格式的地址数组。 
如果端口是 IANA 默认的 DNS 端口（53），则可以省略。

```js
dns.setServers([
  '4.4.4.4',
  '[2001:4860:4860::8888]',
  '4.4.4.4:1053',
  '[2001:4860:4860::8888]:1053'
]);
```

如果提供了无效地址，则会抛出错误。

DNS 查询正在进行时，不得调用 `dns.setServers()` 方法。

[`dns.setServers()`] 方法仅影响 [`dns.resolve()`]、`dns.resolve*()` 和 [`dns.reverse()`]（特别是 [`dns.lookup()`]）。

这个方法很像 [resolve.conf][_resolve_conf]。 
也就是说，如果尝试使用提供的第一个服务器解析会导致 `NOTFOUND` 错误，则 `resolve()` 方法将不会尝试使用提供的后续服务器进行解析。 
仅当较早的 DNS 服务器超时或导致其他一些错误时，才会使用后备 DNS 服务器。



