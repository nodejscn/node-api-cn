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


