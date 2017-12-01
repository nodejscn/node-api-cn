<!-- YAML
added: v0.1.92
-->

* Returns: {net.Socket} Socket 本身。

启用/禁用长连接功能， 并且在第一个长连接探针被发送到一个空闲的 socket 之前可选则配置初始延迟。`enable` 默认为 `false`。

`initialDelay`（毫秒）用来设置接收到最后一个数据包和发送第一个长连接探针之间的延迟。将 initialDelay 设置为 0，则会保持默认值（或之前设置的值）不变。默认是 `0`。
