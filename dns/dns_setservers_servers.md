<!-- YAML
added: v0.11.3
-->
- `servers` {string[]} array of [rfc5952][] formatted addresses

设置IP地址服务器端口在进行DNS解析时可用，`servers`参数是一个[rfc5952][]数组格式的地址。
如果端口是IANA默认端口(53),那么它可以被忽略。

比如:

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

