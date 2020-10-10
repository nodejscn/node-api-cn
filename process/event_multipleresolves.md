<!-- YAML
added: v10.12.0
-->

* `type` {string} 错误类型。`'resolve'` 或 `'reject'` 之一。
* `promise` {Promise} 不止一次`'resolve'`或`'reject'`的 Promise。
* `value` {any} 在原始解析后`'resolve'`或`'reject'`的 Promise 的值。

只要 `Promise` 有以下情况，就会触发 `'multipleResolves'` 事件：

* resolve不止一次。
* reject不止一次。
* resolve后reject。
* reject后resolve。

这对于在使用 Promise 构造函数时跟踪应用程序中的潜在错误非常有用，因为会以静默方式吞没多个解决。 
但是，此事件的发生并不一定表示错误。 
例如，[`Promise.race()`] 可以触发 `'multipleResolves'` 事件。

```js
process.on('multipleResolves', (type, promise, reason) => {
  console.error(type, promise, reason);
  setImmediate(() => process.exit(1));
});

async function main() {
  try {
    return await new Promise((resolve, reject) => {
      resolve('第一次调用');
      resolve('吞没解决');
      reject(new Error('吞没解决'));
    });
  } catch {
    throw new Error('失败');
  }
}

main().then(console.log);
// resolve: Promise { '第一次调用' } '吞没解决'
// reject: Promise { '第一次调用' } Error: 吞没解决
//     at Promise (*)
//     at new Promise (<anonymous>)
//     at main (*)
// 第一次调用
```

