
`triggerId` is the `asyncId` of the resource that caused (or "triggered") the
new resource to initialize and that caused `init` to call. This is different
from `async_hooks.currentId()` that only shows *when* a resource was created,
while `triggerId` shows *why* a resource was created.


The following is a simple demonstration of `triggerId`:

```js
async_hooks.createHook({
  init(asyncId, type, triggerId) {
    const cId = async_hooks.currentId();
    fs.writeSync(
      1, `${type}(${asyncId}): trigger: ${triggerId} scope: ${cId}\n`);
  }
}).enable();

require('net').createServer((conn) => {}).listen(8080);
```

Output when hitting the server with `nc localhost 8080`:

```
TCPWRAP(2): trigger: 1 scope: 1
TCPWRAP(4): trigger: 2 scope: 0
```

The first `TCPWRAP` is the server which receives the connections.

The second `TCPWRAP` is the new connection from the client. When a new
connection is made the `TCPWrap` instance is immediately constructed. This
happens outside of any JavaScript stack (side note: a `currentId()` of `0`
means it's being executed from C++, with no JavaScript stack above it).
With only that information it would be impossible to link resources together in
terms of what caused them to be created, so `triggerId` is given the task of
propagating what resource is responsible for the new resource's existence.

