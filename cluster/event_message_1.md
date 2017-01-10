
* `worker` {cluster.Worker}
* `message` {Object}
* `handle` {undefined|Object}

Emitted when the cluster master receives a message from any worker.

See [child_process event: 'message'][].

Before Node.js v6.0, this event emitted only the message and the handle,
but not the worker object, contrary to what the documentation stated.

If you need to support older versions and don't need the worker object,
you can work around the discrepancy by checking the number of arguments:

```js
cluster.on('message', function(worker, message, handle) {
  if (arguments.length === 2) {
    handle = message;
    message = worker;
    worker = undefined;
  }
  // ...
});
```

