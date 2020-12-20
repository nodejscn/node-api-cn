<!-- YAML
added: v11.13.0
-->

* 返回: {stream.Readable} 包含 V8 堆快照的可读流。

生成当前 V8 堆的快照，并返回可读流，该可读流可用于读取 JSON 序列化表示。 
此 JSON 流格式旨在与 Chrome DevTools 等工具一起使用。 
JSON 模式未记录且特定于V8引擎。
因此，该模式可能从 V8 的一个版本更改为下一个版本。

```js
// 打印堆快照到控制台。
const v8 = require('v8');
const stream = v8.getHeapSnapshot();
stream.pipe(process.stdout);
```

