<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}
* `request` {http.ClientRequest}


在由于 keep-alive 选项而持久化之后，当 `socket` 附加到  `request` 时调用。默认行为是：

```js
socket.ref();
```

该方法可以被一个特定的  `Agent` 基类重写。
