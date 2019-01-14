<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}

当 `socket` 与请求分离并且可以由 `Agent` 保留时调用。 
默认行为是：

```js
socket.setKeepAlive(true, this.keepAliveMsecs);
socket.unref();
return true;
```

此方法可以由特定的 `Agent` 子类重写。 
如果此方法返回一个假值，则将销毁套接字而不是将其保留以用于下一个请求。


