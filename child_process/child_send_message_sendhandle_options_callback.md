<!-- YAML
added: v0.5.9
-->

* `message` {Object}
* `sendHandle` {Handle}
* `options` {Object}
* `callback` {Function}
* Returns: {Boolean}

When an IPC channel has been established between the parent and child (
i.e. when using [`child_process.fork()`][]), the `child.send()` method can be
used to send messages to the child process. When the child process is a Node.js
instance, these messages can be received via the [`process.on('message')`][] event.

For example, in the parent script:

```js
const cp = require('child_process');
const n = cp.fork(`${__dirname}/sub.js`);

n.on('message', (m) => {
  console.log('PARENT got message:', m);
});

n.send({ hello: 'world' });
```

And then the child script, `'sub.js'` might look like this:

```js
process.on('message', (m) => {
  console.log('CHILD got message:', m);
});

process.send({ foo: 'bar' });
```

Child Node.js processes will have a [`process.send()`][] method of their own that
allows the child to send messages back to the parent.

There is a special case when sending a `{cmd: 'NODE_foo'}` message. All messages
containing a `NODE_` prefix in its `cmd` property are considered to be reserved
for use within Node.js core and will not be emitted in the child's
[`process.on('message')`][] event. Rather, such messages are emitted using the
`process.on('internalMessage')` event and are consumed internally by Node.js.
Applications should avoid using such messages or listening for
`'internalMessage'` events as it is subject to change without notice.

The optional `sendHandle` argument that may be passed to `child.send()` is for
passing a TCP server or socket object to the child process. The child will
receive the object as the second argument passed to the callback function
registered on the [`process.on('message')`][] event. Any data that is received
and buffered in the socket will not be sent to the child.

The `options` argument, if present, is an object used to parameterize the
sending of certain types of handles. `options` supports the following
properties:

  * `keepOpen` - A Boolean value that can be used when passing instances of
    `net.Socket`. When `true`, the socket is kept open in the sending process.
    Defaults to `false`.

The optional `callback` is a function that is invoked after the message is
sent but before the child may have received it.  The function is called with a
single argument: `null` on success, or an [`Error`][] object on failure.

If no `callback` function is provided and the message cannot be sent, an
`'error'` event will be emitted by the [`ChildProcess`][] object. This can happen,
for instance, when the child process has already exited.

`child.send()` will return `false` if the channel has closed or when the
backlog of unsent messages exceeds a threshold that makes it unwise to send
more. Otherwise, the method returns `true`. The `callback` function can be
used to implement flow control.

