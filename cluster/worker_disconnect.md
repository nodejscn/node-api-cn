<!-- YAML
added: v0.7.7
changes:
  - version: v7.3.0
    pr-url: https://github.com/nodejs/node/pull/10019
    description: This method now returns a reference to `worker`.
-->

* Returns: {Worker} 一个 `worker` 的引用。

在一个工作进程内，调用此方法会关闭所有的server，并等待这些server的 `'close'`事件执行，然后关闭IPC管道。

在主进程内，会给工作进程发送一个内部消息，导致工作进程自身调用`.disconnect()`。

会设置`.exitedAfterDisconnect` 。

需要注意的是，当一个server关闭后，它将不再接收新的连接，但新连接会被其他正在监听的工作进程接收。已建立的连接可以正常关闭。当所有连接都关闭后，通往该工作进程的IPC管道将会关闭，允许工作进程优雅地死掉，详见 [`server.close()`][]。

以上情况只针对服务端连接，工作进程不会自动关闭客户端连接，disconnect方法在退出前并不会等待客户端连接关闭。

需要注意的是，我们这里的方法是[`disconnect`][]，同时还有一个不一样的方法`process.disconnect`，大家不要混淆了。

由于长时间运行的服务端连接可能导致工作进程的disconnect方法阻塞，我们可以采用发送消息的方法，让应用采取相应的动作来关闭连接。也可以通过设置timeout，当`'disconnect'`事件在某段时间后仍没有触发时关闭工作进程。

```js
if (cluster.isMaster) {
  const worker = cluster.fork();
  let timeout;

  worker.on('listening', (address) => {
    worker.send('shutdown');
    worker.disconnect();
    timeout = setTimeout(() => {
      worker.kill();
    }, 2000);
  });

  worker.on('disconnect', () => {
    clearTimeout(timeout);
  });

} else if (cluster.isWorker) {
  const net = require('net');
  const server = net.createServer((socket) => {
    // 连接永远不会结束
  });

  server.listen(8000);

  process.on('message', (msg) => {
    if (msg === 'shutdown') {
      // 将所有与服务器的连接优雅关闭
    }
  });
}
```
