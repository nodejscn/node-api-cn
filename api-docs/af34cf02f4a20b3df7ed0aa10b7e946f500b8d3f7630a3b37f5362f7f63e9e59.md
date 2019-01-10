<!-- YAML
added: v0.1.16
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9587
    description: Added `external` to the returned object.
-->

* 返回: {Object}
    * `rss` {integer}
    * `heapTotal` {integer}
    * `heapUsed` {integer}
    * `external` {integer}

`process.memoryUsage()`方法返回Node.js进程的内存使用情况的对象，该对象每个属性值的单位为字节。

例如:

```js
console.log(process.memoryUsage());
```

会得到:

<!-- eslint-skip -->
```js
{
  rss: 4935680,
  heapTotal: 1826816,
  heapUsed: 650472,
  external: 49879
}
```

`heapTotal` 和 `heapUsed` 代表V8的内存使用情况。
`external`代表V8管理的，绑定到Javascript的C++对象的内存使用情况。
`rss`, 驻留集大小, 是给这个进程分配了多少物理内存(占总分配内存的一部分)
这些物理内存中包含堆，栈，和代码段。

对象，字符串，闭包等存于堆内存。
变量存于栈内存。
实际的JavaScript源代码存于代码段内存。
