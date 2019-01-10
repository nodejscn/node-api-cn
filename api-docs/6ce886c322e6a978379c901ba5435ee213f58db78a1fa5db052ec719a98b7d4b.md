<!-- YAML
added: v10.6.0
-->
* `servers` {string[]} array of [rfc5952][] formatted addresses

Sets the IP address and port of servers to be used when performing DNS
resolution. The `servers` argument is an array of [rfc5952][] formatted
addresses. If the port is the IANA default DNS port (53) it can be omitted.

```js
dnsPromises.setServers([
  '4.4.4.4',
  '[2001:4860:4860::8888]',
  '4.4.4.4:1053',
  '[2001:4860:4860::8888]:1053'
]);
```

An error will be thrown if an invalid address is provided.

The `dnsPromises.setServers()` method must not be called while a DNS query is in
progress.

Note that this method works much like

That is, if attempting to resolve with the first server provided results in a
`NOTFOUND` error, the `resolve()` method will *not* attempt to resolve with
subsequent servers provided. Fallback DNS servers will only be used if the
earlier ones time out or result in some other error.

