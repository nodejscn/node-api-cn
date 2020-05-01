<!-- YAML
added:
 - v13.2.0
 - v12.16.0
-->

* `line` {Buffer} ASCII 的文本行，采用 NSS 的 `SSLKEYLOGFILE` 格式。
* `tlsSocket` {tls.TLSSocket} 生成 keylog 的 `tls.TLSSocket` 实例。

当此 agent 管理的连接生成或接收到密钥材料时（通常在握手完成之前，但不一定），则触发 `keylog` 事件。 
此密钥材料可以保存起来用以调试，因为它可以对捕获的 TLS 通信进行解密。 
每个 socket 可以被多次触发。

一个典型的用例是，将接收到的文本行附加到一个普通的文本文件，该文件随后可被软件（例如 Wireshark）进行解密通信：

```js
// ...
https.globalAgent.on('keylog', (line, tlsSocket) => {
  fs.appendFileSync('/tmp/ssl-keys.log', line, { mode: 0o600 });
});
```

