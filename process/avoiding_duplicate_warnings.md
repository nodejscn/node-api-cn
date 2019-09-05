
作为最佳实践，警告应该在每个进程中最多发出一次。
为了达到上述的要求，推荐在使用`emitWarning()`之前用一个简单的布尔值做判断，如下例所示：

```js
function emitMyWarning() {
  if (!emitMyWarning.warned) {
    emitMyWarning.warned = true;
    process.emitWarning('只警告一次');
  }
}
emitMyWarning();
// 触发: (node: 56339) Warning: 只警告一次
emitMyWarning();
// 什么都没触发。
```

