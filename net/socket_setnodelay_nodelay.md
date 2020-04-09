<!-- YAML
added: v0.1.90
-->

* `noDelay` {boolean} **默认值:** `true`。
* 返回: {net.Socket} Socket 本身。

启用或禁用 Nagle 算法的使用。

当TCP 连接被创建时，它会启用 Nagle 算法。

Nagle 算法会延迟数据，然后再通过网络发送数据。 
它会尝试以延迟为代价优化吞吐量。

为 `noDelay` 传入 `true` 或不传参数，则会禁用 Nagle 的 socket 算法。 
为 `noDelay` 传入 `false` 则会启用 Nagle 算法。
