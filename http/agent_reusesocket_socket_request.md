<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}
* `request` {http.ClientRequest}

由于 keep-alive 选项被保持持久化, 在 `socket` 附加到 `request` 时调用. 默认行为是:

```js
socket.ref();
```

这个方法可以被一个特定的 `Agent` 子类重写.
