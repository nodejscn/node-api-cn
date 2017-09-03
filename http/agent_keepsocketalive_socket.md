<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}

在 `socket` 被请求分离的时候调用, 可能被代理持续使用. 默认行为:
```js
socket.unref();
socket.setKeepAlive(agent.keepAliveMsecs);
```

这个方法可以被一个特定的 `Agent` 子类重写. 如果这个方法返回假值, socket 会被销毁而不是
在下一次请求时持续使用.
