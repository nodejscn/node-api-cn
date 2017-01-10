
As a user is typing input into the REPL prompt, pressing the `<enter>` key will
send the current line of input to the `eval` function. In order to support
multi-line input, the eval function can return an instance of `repl.Recoverable`
to the provided callback function:

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

