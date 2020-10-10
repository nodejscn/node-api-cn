<!-- YAML
added: v10.5.0
-->

* {boolean}

如果此代码不在 [`Worker`] 线程内运行，则为 `true`。

```js
const { Worker, isMainThread } = require('worker_threads');

if (isMainThread) {
  // 这会在工作线程实例中重新加载当前文件。
  new Worker(__filename);
} else {
  console.log('在工作线程中');
  console.log(isMainThread);  // 打印 'false'。
}
```

