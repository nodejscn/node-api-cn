
* `targetObject` {Object}
* `constructorOpt` {Function}

在 `targetObject` 上创建一个 `.stack` 属性，当访问时返回一个表示代码中调用 `Error.captureStackTrace()` 的位置的字符串。

```js
const myObject = {};
Error.captureStackTrace(myObject);
myObject.stack;  // 类似 `new Error().stack`
```

The first line of the trace will be prefixed with `${myObject.name}: ${myObject.message}`.

可选的 `constructorOpt` 参数接受一个函数。
如果提供了，则 `constructorOpt` 之上包括自身在内的全部栈帧都会被生成的堆栈跟踪省略。

`constructorOpt` 参数用在向最终用户隐藏错误生成的具体细节时非常有用。例如：


```js
function MyError() {
  Error.captureStackTrace(this, MyError);
}

// 没传入 MyError 到 captureStackTrace，MyError 帧会显示在 .stack 属性。
// 通过传入构造函数，可以省略该帧，且保留其下面的所有帧。
new MyError().stack;
```

