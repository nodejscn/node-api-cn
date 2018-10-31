<!-- YAML
added: v0.9.4
-->

* `stream` {Stream} 老版本的可读流。
* 返回: {this}

在 Node.js v0.10 之前，流没有实现当前定义的所有的流模块 API。（详见[兼容性][Compatibility]）

当使用老版本的 Node.js 时，只能触发 [`'data'`] 事件或调用 [`stream.pause()`][stream-pause] 方法，可以使用 `readable.wrap()` 创建老版本的流作为数据源。

现在几乎无需使用 `readable.wrap()`，该方法主要用于老版本的 Node.js 应用和库。

例子：

```js
const { OldReader } = require('./old-api-module.js');
const { Readable } = require('stream');
const oreader = new OldReader();
const myReader = new Readable().wrap(oreader);

myReader.on('readable', () => {
  myReader.read(); // 各种操作。
});
```

