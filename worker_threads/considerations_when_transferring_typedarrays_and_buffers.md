
所有的 `TypedArray` 和 `Buffer` 实例都是基于 `ArrayBuffer` 之上的视图。
也就是说，尽管 `TypedArray` 和 `Buffer` 对象提供操作数据的方法，
但实际存放数据的是他们的 `ArrayBuffer`。
可以为同一个 `ArrayBuffer` 实例创建多个视图。
但需要特别注意，当使用 `transferList` 转移一个 `ArrayBuffer` 时
会导致所有基于此的 `TypedArray` 和 `Buffer` 实例变得无法使用。

```js
const ab = new ArrayBuffer(10);

const u1 = new Uint8Array(ab);
const u2 = new Uint16Array(ab);

console.log(u2.length);  // 打印 5

port.postMessage(u1, [u1.buffer]);

console.log(u2.length);  // 打印 0
```

对于 `Buffer` 实例，确切地说，它的 `ArrayBuffer` 是否可以被转移还是克隆，
完全取决于该实例的创建方式，无法一概而论。

`ArrayBuffer` 可以用 [`markAsUntransferable()`][] 来声明它总是应该被克隆并且从不会被转移。

根据一个 `Buffer` 实例如何被创建，它可以拥有自己的 `ArrayBuffer` 或没有。
除非已知该 `Buffer` 实例拥有它否则 `ArrayBuffer` 无法被转移。
需要注意，对于从内部的 `Buffer` 内存池创建的实例
（例如使用 `Buffer.from()` 或 `Buffer.allocUnsafe()`），
它们将总是被克隆而无法被转移，并且会克隆整个 `Buffer` 内存池发送。
这种行为可能会导致不可预料的高内存占用和安全问题。

关于 `Buffer` 内存池的更多内容参考 [`Buffer.allocUnsafe()`][]。

如果一个 `Buffer` 实例使用 `Buffer.alloc()` 或 `Buffer.allocUnsafeSlow()` 创建，
那么它的 `ArrayBuffer` 总是可以被转移，
不过这么做会导致其它基于此 `ArrayBuffer` 的视图变得无法使用。

