<!-- YAML
added: v0.7.7
-->

Similar to the `cluster.on('disconnect')` event, but specific to this worker.

```js
cluster.fork().on('disconnect', () => {
  // Worker has disconnected
});
```

