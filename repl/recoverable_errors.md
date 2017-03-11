假如一个用户键入信息到REPL提示行，按下`<enter>`键将会把当前行的输入发送到`eval`函数。
为了支持多行输入，`eval`函数可以返回一个`repl.Recoverable`的实例来提供回调功能：

```js
function eval(cmd, context, filename, callback) {
  var result;
  try {
    result = vm.runInThisContext(cmd);
  } catch (e) {
    if (isRecoverableError(e)) {
      return callback(new repl.Recoverable(e));
    }
  }
  callback(null, result);
}

function isRecoverableError(error) {
  if (error.name === 'SyntaxError') {
    return /^(Unexpected end of input|Unexpected token)/.test(error.message);
  }
  return false;
}
```

