<!-- YAML
added: v0.9.4
-->

* `stream` {Stream} 一个老版本的readable stream

Node.js在v0.10版本之前的流没有实现当前定义的所有流模块的API.(查看更多兼容性信息 [Compatibility][]
)

当使用老版本的Node.js库来触发[`'data'`][]事件和[`stream.pause()`][stream-pause]方法仅是建议性的，
`readable.wrap()`方法能创建一个把老版本的流作为数据源的[Readable][] stream。

几乎没有必要使用`readable.wrap()`，但是这个方法已经为老版本的Node.js应用和一些库提供了方便。

例子：

```js
const { OldReader } = require('./old-api-module.js');
const { Readable } = require('stream');
const oreader = new OldReader();
const myReader = new Readable().wrap(oreader);

myReader.on('readable', () => {
  myReader.read(); // etc.
});
```

