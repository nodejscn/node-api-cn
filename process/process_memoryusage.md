<!-- YAML
added: v0.1.16
changes:
  - version: v13.9.0
    pr-url: https://github.com/nodejs/node/pull/31550
    description: Added `arrayBuffers` to the returned object.
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9587
    description: Added `external` to the returned object.
-->

* 返回: {Object}
  * `rss` {integer}
  * `heapTotal` {integer}
  * `heapUsed` {integer}
  * `external` {integer}
  * `arrayBuffers` {integer}

`process.memoryUsage()` 方法返回 Node.js 进程的内存使用情况的对象，该对象每个属性值的单位为字节。

例如：

```js
console.log(process.memoryUsage());
```

会得到：

<!-- eslint-skip -->
```js
{
  rss: 4935680,
  heapTotal: 1826816,
  heapUsed: 650472,
  external: 49879,
  arrayBuffers: 9386
}
```

* `heapTotal` 和 `heapUsed` 代表 V8 的内存使用情况。
* `external` 代表 V8 管理的，绑定到 Javascript 的 C++ 对象的内存使用情况。
* `rss` 是驻留集大小, 是给这个进程分配了多少物理内存（占总分配内存的一部分），包含所有的 C++ 和 JavaScript 对象与代码。
* `arrayBuffers` 指分配给 `ArrayBuffer` 和 `SharedArrayBuffer` 的内存，包括所有的 Node.js [`Buffer`]。 
  这也包含在 `external` 值中。 
  当 Node.js 用作嵌入式库时，此值可能为 `0`，因为在这种情况下可能无法跟踪 `ArrayBuffer` 的分配。

使用 [`Worker`] 线程时，`rss` 将会是一个对整个进程有效的值，而其他字段只指向当前线程。

