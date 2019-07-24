
`Error` 的一个子类，表明提供的参数不是一个被允许的类型。
例如，将一个函数传给一个期望字符串的参数会被视为一个 `TypeError`。

```js
require('url').parse(() => { });
// 抛出 TypeError，因为它期望的是一个字符串
```

Node.js 会生成并以参数校验的形式立即抛出 `TypeError` 实例。

