<!-- YAML
added: v8.9.3
-->

* `payload` {Buffer|TypedArray|DataView} Optional ping payload.
* `callback` {Function}
* Returns: {boolean}

Sends a `PING` frame to the connected HTTP/2 peer. A `callback` function must
be provided. The method will return `true` if the `PING` was sent, `false`
otherwise.

The maximum number of outstanding (unacknowledged) pings is determined by the
`maxOutstandingPings` configuration option. The default maximum is 10.

If provided, the `payload` must be a `Buffer`, `TypedArray`, or `DataView`
containing 8 bytes of data that will be transmitted with the `PING` and
returned with the ping acknowledgement.

The callback will be invoked with three arguments: an error argument that will
be `null` if the `PING` was successfully acknowledged, a `duration` argument
that reports the number of milliseconds elapsed since the ping was sent and the
acknowledgement was received, and a `Buffer` containing the 8-byte `PING`
payload.

```js
session.ping(Buffer.from('abcdefgh'), (err, duration, payload) => {
  if (!err) {
    console.log(`Ping acknowledged in ${duration} milliseconds`);
    console.log(`With payload '${payload.toString()}`);
  }
});
```

If the `payload` argument is not specified, the default payload will be the
64-bit timestamp (little endian) marking the start of the `PING` duration.

