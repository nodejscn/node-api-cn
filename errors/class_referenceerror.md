
`Error` 的一个子类，表明试图访问一个未定义的变量。
这些错误通常表明代码有拼写错误或程序已损坏。

虽然客户端代码可能产生和传播这些错误，但在实践中，只有 V8 引擎会这么做。

```js
doesNotExist;
  // 抛出 ReferenceError，在这个程序中 doesNotExist 不是一个变量。
```

`ReferenceError` 实例有一个 `error.arguments` 属性，其值是一个只有单个元素（一个代表未定义的变量的字符串）的数组。

```js
const assert = require('assert');
try {
  doesNotExist;
} catch(err) {
  assert(err.arguments[0], 'doesNotExist');
}
```

除非应用程序是动态生成并运行的代码，否则 `ReferenceError` 实例应该始终被视为代码中或其依赖中的错误。

