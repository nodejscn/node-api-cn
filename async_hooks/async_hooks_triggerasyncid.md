
* 返回 {number} 负责调用当前正在执行的回调的资源的ID。

例如:

```js
const server = net.createServer((conn) => {
  // 导致（或触发）此回调被调用的资源是新连接的资源。 因此，triggerAsyncId()的返回值是"conn"的asyncId。
  async_hooks.triggerAsyncId();

}).listen(port, () => {
  // Even though all callbacks passed to .listen() are wrapped in a nextTick()
  // the callback itself exists because the call to the server's .listen()
  // was made. So the return value would be the ID of the server.
  // 即使所有传递给.listen()的回调都包装在nextTick()中，但是因为对服务器.listen()的调用造成回调本身存在。
  // 因此返回值是服务器的ID。
  async_hooks.triggerAsyncId();
});
```

