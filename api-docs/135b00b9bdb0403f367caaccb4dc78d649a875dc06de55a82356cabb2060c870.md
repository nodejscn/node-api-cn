<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}

当新建一个工作进程后，工作进程应当响应一个online消息给主进程。当主进程收到online消息后触发这个事件。
 `'fork'` 事件和 `'online'`事件的不同之处在于，前者是在主进程新建工作进程后触发，而后者是在工作进程运行的时候触发。

```js
cluster.on('online', (worker) => {
  console.log('Yay, the worker responded after it was forked');
});
```

