
* `asyncId` {number} 异步资源的唯一ID
* `type` {string} 异步资源的类型
* `triggerAsyncId` {number} 异步资源创建时执行上下文中异步资源的唯一ID
* `resource` {Object} 代表异步操作的资源参照，必须在 _destroy_ 期间释放

当构造有 _可能_ 触发异步事件的类时调用。这并 _不_ 意味着实例必须在调用`destroy`之前调用`before`/`after`，只有当可能性存在时才这么做。

可以通过打开资源，然后在使用资源之前关闭资源来观察此行为。 以下代码段演示了这一点。

```js
require('net').createServer().listen(function() { this.close(); });
// 或
clearTimeout(setTimeout(() => {}, 10));
```

每个新资源都被分配了一个唯一的ID。
