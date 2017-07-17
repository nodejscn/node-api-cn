<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}


当 `socket` 从请求中分离并且可以被 Agent 持久化时调用。默认行为如下：

```js
socket.unref();
socket.setKeepAlive(agent.keepAliveMsecs);
```

该方法可以被一个特定的 `Agent` 基类重写。如果该方法返回一个 flasy 值（即转换为 Boolean 后为 false 的值），socket 会被销毁，而不是持续存在等待下一个请求来使用。
