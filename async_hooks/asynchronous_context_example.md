
The following is an example with additional information about the calls to
`init` between the `before` and `after` calls, specifically what the
callback to `listen()` will look like. The output formatting is slightly more
elaborate to make calling context easier to see.

```js
let indent = 0;
async_hooks.createHook({
  init(asyncId, type, triggerAsyncId) {
    const eid = async_hooks.executionAsyncId();
    const indentStr = ' '.repeat(indent);
    fs.writeSync(
      1,
      `${indentStr}${type}(${asyncId}):` +
      ` trigger: ${triggerAsyncId} execution: ${eid}\n`);
  },
  before(asyncId) {
    const indentStr = ' '.repeat(indent);
    fs.writeSync(process.stdout.fd, `${indentStr}before:  ${asyncId}\n`);
    indent += 2;
  },
  after(asyncId) {
    indent -= 2;
    const indentStr = ' '.repeat(indent);
    fs.writeSync(process.stdout.fd, `${indentStr}after:  ${asyncId}\n`);
  },
  destroy(asyncId) {
    const indentStr = ' '.repeat(indent);
    fs.writeSync(process.stdout.fd, `${indentStr}destroy:  ${asyncId}\n`);
  },
}).enable();

require('net').createServer(() => {}).listen(8080, () => {
  // Let's wait 10ms before logging the server started.
  setTimeout(() => {
    console.log('>>>', async_hooks.executionAsyncId());
  }, 10);
});
```

Output from only starting the server:

```console
TCPSERVERWRAP(5): trigger: 1 execution: 1
TickObject(6): trigger: 5 execution: 1
before:  6
  Timeout(7): trigger: 6 execution: 6
after:   6
destroy: 6
before:  7
>>> 7
  TickObject(8): trigger: 7 execution: 7
after:   7
before:  8
after:   8
```

As illustrated in the example, `executionAsyncId()` and `execution` each specify
the value of the current execution context; which is delineated by calls to
`before` and `after`.

Only using `execution` to graph resource allocation results in the following:

```console
  root(1)
     ^
     |
TickObject(6)
     ^
     |
 Timeout(7)
```

The `TCPSERVERWRAP` is not part of this graph, even though it was the reason for
`console.log()` being called. This is because binding to a port without a host
name is a *synchronous* operation, but to maintain a completely asynchronous
API the user's callback is placed in a `process.nextTick()`. Which is why
`TickObject` is present in the output and is a 'parent' for `.listen()`
callback.

The graph only shows *when* a resource was created, not *why*, so to track
the *why* use `triggerAsyncId`. Which can be represented with the following
graph:

```console
 bootstrap(1)
     |
     ˅
TCPSERVERWRAP(5)
     |
     ˅
 TickObject(6)
     |
     ˅
  Timeout(7)
```

