<!-- YAML
added: v0.1.26
changes:
  - version: v1.8.1
    pr-url: https://github.com/nodejs/node/pull/1077
    description: 支持 `callback` 后面的额外参数。
-->

* `callback` {Function}
* `...args` {any} 当调用 `callback` 时传入的额外参数。

`process.nextTick()` 会添加 `callback` 到下一个时间点队列。
在 JavaScript 堆栈上的当前操作运行完成之后，且允许事件循环继续之前，此队列会被完全耗尽。 
如果递归地调用 `process.nextTick()`，则可以创建无限的循环。 
有关更多背景信息，请参见[事件循环][Event Loop]指南。

```js
console.log('开始');
process.nextTick(() => {
  console.log('下一个时间点的回调');
});
console.log('调度');
// 输出:
// 开始
// 调度
// 下一个时间点的回调
```

这在开发 API 时非常重要，可以在构造对象之后但在发生任何 I/O 之前，为用户提供分配事件句柄的机会：


```js
function MyThing(options) {
  this.setupOptions(options);

  process.nextTick(() => {
    this.startDoingStuff();
  });
}

const thing = new MyThing();
thing.getReadyForStuff();

// thing.startDoingStuff() 现在（而不是在之前）会被调用。
```

对于 100% 同步或 100% 异步的 API，此方法也非常重要。
参考以下示例：

```js
// 警告！不要这样使用！这是不安全的！
function maybeSync(arg, cb) {
  if (arg) {
    cb();
    return;
  }

  fs.stat('file', cb);
}
```

此 API 是不安全的，因为在以下情况中：

```js
const maybeTrue = Math.random() > 0.5;

maybeSync(maybeTrue, () => {
  foo();
});

bar();
```

不清楚 `foo()` 和 `bar()` 哪个会先被调用。

以下方法则更好：

```js
function definitelyAsync(arg, cb) {
  if (arg) {
    process.nextTick(cb);
    return;
  }

  fs.stat('file', cb);
}
```

