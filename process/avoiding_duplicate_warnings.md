
作为最佳实践，警告应该在每个进程中最多发出一次。
为了达到上述的要求，推荐在使用`emitWarning()`之前用一个简单的布尔值做判断，如下例所示：

```js
function emitMyWarning() {
  if (!emitMyWarning.warned) {
    emitMyWarning.warned = true;
    process.emitWarning('Only warn once!');
  }
}
emitMyWarning();
// Emits: (node: 56339) Warning: Only warn once!
emitMyWarning();
// Emits nothing
```

