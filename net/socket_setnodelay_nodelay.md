<!-- YAML
added: v0.1.90
-->

* `noDelay` {boolean} **默认值:** `true`。
* 返回: {net.Socket} Socket 本身。

禁止 Nagle 算法。默认情况下 TCP 连接使用 Nagle 算法，在发送之前缓冲数据。将 `noDelay` 设置为 `true` 将会在每次 `socket.write()` 被调用的时候立即发送数据。
