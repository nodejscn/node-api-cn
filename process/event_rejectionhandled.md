<!-- YAML
added: v1.4.1
-->

如果有Promise被rejected，并且此Promise在Nodje.js事件循环的下次轮询及之后期间，被绑定了一个错误处理器[`例如使用promise.catch()`][])，
会触发`'rejectionHandled'`事件。

此事件监听器的回调函数使用Rejected的`Promise`引用，作为唯一入参。

`Promise`对象应该已经在`'unhandledRejection'`事件触发时被处理，但是在被处理过程中获得了一个rejection处理器。

对于`Promise` chain，没有概念表明在 Promise chain的哪个地方，所有的rejections总是会被处理。
由于本来就是异步的，一个`Promise` rejection可以在将来的某个时间点被处理-可能要远远晚于`'unhandledRejection'`事件被触发及处理的时间。

另一种表述的方式就是，与使用同步代码时会出现不断增长的未处理异常列表不同，使用Promises时，未处理异常列表可能会出现增长然后收缩的情况。

在同步代码情况下，当未处理异常列表增长时，会触发`'uncaughtException'`事件。

在异步代码情况下，当未处理异常列表增长时，会触发`'uncaughtException'`事件，当未处理列表收缩时，会触发`'rejectionHandled'`事件。

例如:

```js
const unhandledRejections = new Map();
process.on('unhandledRejection', (reason, p) => {
  unhandledRejections.set(p, reason);
});
process.on('rejectionHandled', (p) => {
  unhandledRejections.delete(p);
});
```

在上述例子中，`unhandledRejections` `Map`会随着时间增加和缩减，表明rejections开始是未被处理状态，然后变成已处理状态。
可以定时(对于需长期运行的应用，这个可能是最好的方式)或当进程结束时(对脚本的应用可能是最方便的)，在错误日志中记录这些错误信息。

