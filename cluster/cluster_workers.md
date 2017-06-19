<!-- YAML
added: v0.7.0
-->

* {Object}

这是一个哈希表，储存了活跃的工作进程对象，`id`作为key。有了它，可以方便地遍历所有工作进程。只能在主进程中调用。

工作进程断开连接以及退出后，将会从cluster.workers里面移除。这两个事件的先后顺序并不能预先确定，但可以保证的是，
cluster.workers的移除工作在`'disconnect'` 和 `'exit'`两个事件中的最后一个触发之前完成。

```js
// Go through all workers
function eachWorker(callback) {
  for (const id in cluster.workers) {
    callback(cluster.workers[id]);
  }
}
eachWorker((worker) => {
  worker.send('big announcement to all workers');
});
```
使用工作进程的id来进行定位索引是最方便的！

```js
socket.on('data', (id) => {
  const worker = cluster.workers[id];
});
```

