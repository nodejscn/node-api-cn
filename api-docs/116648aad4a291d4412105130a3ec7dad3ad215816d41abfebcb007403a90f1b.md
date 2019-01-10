<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}

当 `socket` 从请求中分离且可被 `Agent` 继续使用时调用。

默认行为是：

```js
socket.setKeepAlive(true, this.keepAliveMsecs);
socket.unref();
return true;
```

该方法可被 `Agent` 子类重写。
如果方法返回 `false` 值, 则 socket 会被销毁而不是在下一次请求时持续使用。

