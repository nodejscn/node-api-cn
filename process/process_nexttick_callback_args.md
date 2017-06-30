<!-- YAML
added: v0.1.26
changes:
  - version: v1.8.1
    pr-url: https://github.com/nodejs/node/pull/1077
    description: Additional arguments after `callback` are now supported.
-->

* `callback` {Function}
* `...args` {any} 调用 `callback`时传递给它的额外参数

`process.nextTick()`方法将 `callback` 添加到"next tick 队列"。
一旦当前事件轮询队列的任务全部完成，在next tick队列中的所有callbacks会被依次调用。

这种方式不是[`setTimeout(fn, 0)`][]的别名。它更加有效率。事件轮询随后的ticks 调用，会在任何I/O事件（包括定时器）之前运行。

```js
console.log('start');
process.nextTick(() => {
  console.log('nextTick callback');
});
console.log('scheduled');
// Output:
// start
// scheduled
// nextTick callback
```

此方法在开发如下API时非常重要：在对象构造好但还没有任何I/O发生*之前*，想给用户机会来指定某些事件处理器。

```js
function MyThing(options) {
  this.setupOptions(options);

  process.nextTick(() => {
    this.startDoingStuff();
  });
}

const thing = new MyThing();
thing.getReadyForStuff();

// thing.startDoingStuff() gets called now, not before.
```

对于100%同步或100%异步的API，此方法也非常重要。考虑如下例子：

```js
// WARNING!  DO NOT USE!  BAD UNSAFE HAZARD!
function maybeSync(arg, cb) {
  if (arg) {
    cb();
    return;
  }

  fs.stat('file', cb);
}
```

在如下场景中这个API是危险的：

```js
const maybeTrue = Math.random() > 0.5;

maybeSync(maybeTrue, () => {
  foo();
});

bar();
```

因为不清楚`foo()` 或 `bar()` 哪个会被先调用。

如下方式要更好一些:

```js
function definitelyAsync(arg, cb) {
  if (arg) {
    process.nextTick(cb);
    return;
  }

  fs.stat('file', cb);
}
```

*注意*： 每次事件轮询后，在额外的I/O执行**前**，next tick队列都会优先执行。
递归调用nextTick callbacks 会阻塞任何I/O操作，就像一个`while(true);` 循环一样。