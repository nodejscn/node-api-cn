<!-- YAML
added: v0.1.90
-->

禁止Nagele算法。默认TCP连接使用Nagle算法，它们在发送数据之前先缓存。
设置`noDelay`为`true`将在`socket.write()`每次被调用时，立即发送数据。
`noDelay` 默认为 `true`.

返回 `socket`.

