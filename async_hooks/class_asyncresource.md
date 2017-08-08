
`AsyncResource`类被设计用来扩展内嵌的异步资源。使用该类，用户可以轻易触发他们自己的资源的终身事件。

当`AsyncResource`实例化时，`init`钩将被触发。

`before`/`after`回调释放的顺序和调用顺序相同是很重要的。否则将发生不可恢复的异常，node将中止。

以下是`AsyncResource`API的概述。

```js
const { AsyncResource } = require('async_hooks');

// AsyncResource()用来扩展内嵌的异步资源。当新的`AsyncResource`实例化时，`init`也将被触发。
// 如果忽视triggerAsyncId，那么将使用async_hook.executionAsyncId()
const asyncResource = new AsyncResource(type, triggerAsyncId);

// 在回调前调用AsyncHooks。
asyncResource.emitBefore();

// 在回调后调用AsyncHooks。
asyncResource.emitAfter();

// 在回调销毁时调用AsyncHooks。
asyncResource.emitDestroy();

// 返回分配给异步资源实例的唯一ID。
asyncResource.asyncId();

// 返回异步资源实例的触发器ID。
asyncResource.triggerAsyncId();
```

