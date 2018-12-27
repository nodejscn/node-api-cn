<!-- YAML
added: v10.12.0
-->

* `type` {string} 错误类型。`'resolve'` 或 `'reject'` 之一。
* `promise` {Promise} resolve 或 reject 超过一次的 promise。
* `value` {any} promise resolve 或 rejecte 的值。

当 `Promise` 有以下情况时会触发 `'multipleResolves'` 事件：

* resolve 超过一次。
* rejecte 超过一次。
* resolve 之后再 rejecte。
* reject 之后再 resolve。

主要用于使用 promise 时追踪错误。

```js
process.on('multipleResolves', (type, promise, reason) => {
  console.error(type, promise, reason);
  setImmediate(() => process.exit(1));
});

async function main() {
  try {
    return await new Promise((resolve, reject) => {
      resolve('第一次调用');
      resolve('调用 resolve');
      reject(new Error('调用 reject'));
    });
  } catch {
    throw new Error('出错');
  }
}

main().then(console.log);
// resolve: Promise { '第一次调用' } '调用 resolve'
// reject: Promise { '第一次调用' } Error: 调用 reject
//     at Promise (*)
//     at new Promise (<anonymous>)
//     at main (*)
// 第一次调用
```

