
* 继承自: {errors.Error}

表明提供的参数不在函数的可接受值的集合或范围内；无论是一个数字范围，还是在给定的函数参数的选项的集合之外。

```js
require('net').connect(-1);
// 抛出 "RangeError: "port" option should be >= 0 and < 65536: -1"
```

Node.js 将会以参数验证的形式立即地生成并抛出 `RangeError` 实例。

