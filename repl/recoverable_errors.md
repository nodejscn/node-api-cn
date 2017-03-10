
当用户正在 REPL 中输入时，按下 `<enter>` 键会把当前输入行发送到 `eval` 函数。
为了支持多行输入，解释函数可以返回一个 `repl.Recoverable` 实例，用以提供回调函数：

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

