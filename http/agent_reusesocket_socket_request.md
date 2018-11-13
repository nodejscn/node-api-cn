<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}
* `request` {http.ClientRequest}

当 `socket` 因 `keep-alive` 选项保持持久化且被附加到 `request` 时调用。

默认行为是：

```js
socket.ref();
```

该方法可被 `Agent` 子类重写.

