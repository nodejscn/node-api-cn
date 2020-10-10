
* 继承自 {errors.Error}

表明提供的参数不是被允许的类型。
例如，将函数传给期望字符串的参数，则会抛出 `TypeError`。

```js
require('url').parse(() => { });
// 抛出 TypeError，因为它期望的是字符串。
```

Node.js 将会以参数验证的形式立即地生成并抛出 `TypeError` 实例。

