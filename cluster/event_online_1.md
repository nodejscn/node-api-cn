<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}

After forking a new worker, the worker should respond with an online message.
When the master receives an online message it will emit this event.
The difference between `'fork'` and `'online'` is that fork is emitted when the
master forks a worker, and 'online' is emitted when the worker is running.

```js
cluster.on('online', (worker) => {
  console.log('Yay, the worker responded after it was forked');
});
```

