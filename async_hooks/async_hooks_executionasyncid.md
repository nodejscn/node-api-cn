
* 返回 {number} 当前执行上下文的`asyncId`。当调用时用于跟踪非常有用。

例如:

```js
console.log(async_hooks.executionAsyncId());  // 1 - bootstrap
fs.open(path, 'r', (err, fd) => {
  console.log(async_hooks.executionAsyncId());  // 6 - open()
});
```

要注意到`executionAsyncId()`返回的ID和执行时间有关，而不是因果关系(在`triggerAsyncId()`中存在)是很重要的，例如：

```js
const server = net.createServer(function onConnection(conn) {
  //返回服务器的ID，而不是新连接的ID，因为onConnection回调在服务器MakeCallback()的执行范围内运行。
  async_hooks.executionAsyncId();

}).listen(port, function onListening() {
  //返回TickObject(即 process.nextTick())的ID，因为所有传递给.listen()的回调都被包裹在nextTick()中。
  async_hooks.executionAsyncId();
});
```

