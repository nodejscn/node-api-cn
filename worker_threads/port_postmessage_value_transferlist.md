<!-- YAML
added: v10.5.0
changes:
  - version: v14.5.0
    pr-url: https://github.com/nodejs/node/pull/33360
    description: Added `KeyObject` to the list of cloneable types.
  - version: v14.5.0
    pr-url: https://github.com/nodejs/node/pull/33772
    description: Added `FileHandle` to the list of transferable types.
-->

* `value` {any}
* `transferList` {Object[]}

发送一个JavaScript值给一个接收端。
`value` 使用兼容 [HTML结构化克隆算法][] 的方式传输。

它与一般 `JSON` 的显著区别:

* `value` 可以包含循环引用。
* `value` 可以包含一些内建JS类型，例如：`RegExp`, `BigInt`, `Map`, `Set` 等。
* `value` 可以包含基于 `ArrayBuffer` 和 `SharedArrayBuffer` 的类型数组。
* `value` 可以包含 [`WebAssembly.Module`][] 实例。
* `value` 不能包含 native(需C++模块支持的) 对象，
但以下除外：`MessagePort`、[`FileHandle`][] 和 [`KeyObject`][]。

```js
const { MessageChannel } = require('worker_threads');
const { port1, port2 } = new MessageChannel();

port1.on('message', (message) => console.log(message));

const circularData = {};
circularData.foo = circularData;
// 打印: { foo: [Circular] }
port2.postMessage(circularData);
```

`transferList`（转移列表）是一个可以包含 [`ArrayBuffer`][]、[`MessagePort`][] 和[`FileHandle`][] 对象的数组。
被转移（至另一个线程/上下文）后，这些对象（在当前上下文）将无法再被使用（即使他们不被包含在 `value` 中）。
不同于[child processes][]，转移像socket连接这样的句柄(handle)目前尚不支持。

如果 `value` 包含 [`SharedArrayBuffer`][] 实例，
则这些实例（的内存）将可以被另一个线程直接访问。
并且他们无法被放入 `transferList`。

`value` 可以包含 `ArrayBuffer` 实例，但可以不把他们放入
`transferList`；此时，底层内存将被拷贝而非转移。

```js
const { MessageChannel } = require('worker_threads');
const { port1, port2 } = new MessageChannel();

port1.on('message', (message) => console.log(message));

const uint8Array = new Uint8Array([ 1, 2, 3, 4 ]);
// 发送 `uint8Array` 的一份拷贝:
port2.postMessage(uint8Array);
// 不会拷贝数据, 但是 `uint8Array` 无法再被使用
port2.postMessage(uint8Array, [ uint8Array.buffer ]);

// `sharedUint8Array` 的内存可以同时被发送端和接收端访问
const sharedUint8Array = new Uint8Array(new SharedArrayBuffer(4));
port2.postMessage(sharedUint8Array);

// 发送一个 `MessagePort` 给接收者
// 可以被用来让衍生的子工作线程之间互相通信
const otherChannel = new MessageChannel();
port2.postMessage({ port: otherChannel.port1 }, [ otherChannel.port1 ]);
```

由于使用结构化克隆算法来克隆对象，
不可枚举属性、属性访问器、对象原型将无法被保留。
需要特别注意，[`Buffer`][] 对象在接收端会以 [`Uint8Array`][] 类型被读取。

发送后对象会被立即克隆，之后的修改不会造成任何影响。

更多关于此API的序列化和反序列化机制的内容,
参考 [serialization API of the `v8` module][v8.serdes]。

