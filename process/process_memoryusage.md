<!-- YAML
added: v0.1.16
changes:
  - version: v13.9.0
    pr-url: https://github.com/nodejs/node/pull/31550
    description: 添加 `arrayBuffers` 到返回的对象。
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9587
    description: 添加 `external` 到返回的对象。
-->

* 返回: {Object}
  * `rss` {integer}
  * `heapTotal` {integer}
  * `heapUsed` {integer}
  * `external` {integer}
  * `arrayBuffers` {integer}

`process.memoryUsage()` 方法会返回描述 Node.js 进程的内存使用情况（以字节为单位）的对象。

例如：

```js
console.log(process.memoryUsage());
```

会返回：

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
* `external` 代表 V8 管理的绑定到 Javascript 对象的 C++ 对象的内存使用情况。
* `rss`，常驻集大小, 是为进程分配的物理内存（总分配内存的子集）的大小，包括所有的 C++ 和 JavaScript 对象与代码。
* `arrayBuffers` 代表分配给 `ArrayBuffer` 和 `SharedArrayBuffer` 的内存，包括所有的 Node.js [`Buffer`]。 
  这也包含在 `external` 值中。 
  当 Node.js 被用作嵌入式库时，此值可能为 `0`，因为在这种情况下可能无法跟踪 `ArrayBuffer` 的分配。

当使用 [`Worker`] 线程时，`rss` 会是对整个进程都有效的值，而其他字段只代表当前线程。

