
* `asyncId` {number}

When an asynchronous operation is initiated (such as a TCP server receiving a
new connection) or completes (such as writing data to disk) a callback is
called to notify the user. The `before` callback is called just before said
callback is executed. `asyncId` is the unique identifier assigned to the
resource about to execute the callback.

The `before` callback will be called 0 to N times. The `before` callback
will typically be called 0 times if the asynchronous operation was cancelled
or for example if no connections are received by a TCP server. Asynchronous
like the TCP server will typically call the `before` callback multiple times,
while other operations like `fs.open()` will only call it once.


