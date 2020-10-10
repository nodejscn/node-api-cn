<!-- YAML
added: v10.5.0
-->

（工作线程中可用）指代通过主线程中传递过来的数据。
它可以是任意的JavaScript值，通过主线程构造函数中的选项对象的workerData传递。
这个数据类似Web Worker中[`postMessage()`][`port.postMessage()`]机制，它是拷贝传递的（所以如果是较大数据里，不建议通过此方法）。

```js
const { Worker, isMainThread, workerData } = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(__filename, { workerData: 'Hello, world!' });
} else {
  console.log(workerData);  // Prints 'Hello, world!'.
}
```

