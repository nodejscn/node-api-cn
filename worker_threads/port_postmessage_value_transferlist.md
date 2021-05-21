<!-- YAML
added: v10.5.0
changes:
  - version: v15.14.0
    pr-url: https://github.com/nodejs/node/pull/37917
    description: Add 'BlockList' to the list of cloneable types.
  - version: v15.9.0
    pr-url: https://github.com/nodejs/node/pull/37155
    description: Add 'Histogram' types to the list of cloneable types.
  - version: v15.6.0
    pr-url: https://github.com/nodejs/node/pull/36804
    description: Added `X509Certificate` to the list of cloneable types.
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: Added `CryptoKey` to the list of cloneable types.
  - version:
    - v14.5.0
    - v12.19.0
    pr-url: https://github.com/nodejs/node/pull/33360
    description: Added `KeyObject` to the list of cloneable types.
  - version:
    - v14.5.0
    - v12.19.0
    pr-url: https://github.com/nodejs/node/pull/33772
    description: Added `FileHandle` to the list of transferable types.
-->

* `value` {any}
* `transferList` {Object[]}

Sends a JavaScript value to the receiving side of this channel.
`value` is transferred in a way which is compatible with
the [HTML structured clone algorithm][].

In particular, the significant differences to `JSON` are:

* `value` may contain circular references.
* `value` may contain instances of builtin JS types such as `RegExp`s,
  `BigInt`s, `Map`s, `Set`s, etc.
* `value` may contain typed arrays, both using `ArrayBuffer`s
   and `SharedArrayBuffer`s.
* `value` may contain [`WebAssembly.Module`][] instances.
* `value` may not contain native (C++-backed) objects other than:
  * {CryptoKey}s,
  * {FileHandle}s,
  * {Histogram}s,
  * {KeyObject}s,
  * {MessagePort}s,
  * {net.BlockList}s,
  * {net.SocketAddress}es,
  * {X509Certificate}s.

```js
const { MessageChannel } = require('worker_threads');
const { port1, port2 } = new MessageChannel();

port1.on('message', (message) => console.log(message));

const circularData = {};
circularData.foo = circularData;
// Prints: { foo: [Circular] }
port2.postMessage(circularData);
```

`transferList` may be a list of [`ArrayBuffer`][], [`MessagePort`][] and
[`FileHandle`][] objects.
After transferring, they are not usable on the sending side of the channel
anymore (even if they are not contained in `value`). Unlike with
[child processes][], transferring handles such as network sockets is currently
not supported.

If `value` contains [`SharedArrayBuffer`][] instances, those are accessible
from either thread. They cannot be listed in `transferList`.

`value` may still contain `ArrayBuffer` instances that are not in
`transferList`; in that case, the underlying memory is copied rather than moved.

```js
const { MessageChannel } = require('worker_threads');
const { port1, port2 } = new MessageChannel();

port1.on('message', (message) => console.log(message));

const uint8Array = new Uint8Array([ 1, 2, 3, 4 ]);
// This posts a copy of `uint8Array`:
port2.postMessage(uint8Array);
// This does not copy data, but renders `uint8Array` unusable:
port2.postMessage(uint8Array, [ uint8Array.buffer ]);

// The memory for the `sharedUint8Array` is accessible from both the
// original and the copy received by `.on('message')`:
const sharedUint8Array = new Uint8Array(new SharedArrayBuffer(4));
port2.postMessage(sharedUint8Array);

// This transfers a freshly created message port to the receiver.
// This can be used, for example, to create communication channels between
// multiple `Worker` threads that are children of the same parent thread.
const otherChannel = new MessageChannel();
port2.postMessage({ port: otherChannel.port1 }, [ otherChannel.port1 ]);
```

The message object is cloned immediately, and can be modified after
posting without having side effects.

For more information on the serialization and deserialization mechanisms
behind this API, see the [serialization API of the `v8` module][v8.serdes].

