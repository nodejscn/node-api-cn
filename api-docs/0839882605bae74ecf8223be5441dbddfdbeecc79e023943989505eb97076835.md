<!-- YAML
added: v0.1.90
-->

* Returns: {net.Socket} Socket 本身。

当 socket 在 `timeout` 毫秒不活动之后将其设置为超时状态。默认 `net.Socket` 没有超时。

当一个闲置的超时被触发，socket 将会收到一个 [`'timeout'`][] 事件，但连接不会被断开。用户必须手动调用 [`socket.end()`][] 或 [`socket.destroy()`][] 来断开连接。

```js
socket.setTimeout(3000);
socket.on('timeout', () => {
  console.log('socket timeout');
  socket.end();
});
```

如果 `timeout` 是 0，则存在的闲置超时将会被禁止。

可选的 `callback` 参数将会被当作一个时间监听器被添加到 [`'timeout'`][] 事件。
