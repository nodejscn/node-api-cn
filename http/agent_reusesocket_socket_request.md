<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}
* `request` {http.ClientRequest}

由于 keep-alive 选项而在持久化后将 `socket` 附加到 `request` 时调用。 
默认行为是：

```js
socket.ref();
```

此方法可以由特定的 `Agent` 子类重写。

