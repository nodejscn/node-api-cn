
As of Node.js v0.10, [`dgram.Socket#bind()`][] changed to an asynchronous
execution model. Legacy code that assumes synchronous behavior, as in the
following example:

```js
const s = dgram.createSocket('udp4');
s.bind(1234);
s.addMembership('224.0.0.114');
```

Must be changed to pass a callback function to the [`dgram.Socket#bind()`][]
function:

```js
const s = dgram.createSocket('udp4');
s.bind(1234, () => {
  s.addMembership('224.0.0.114');
});
```

