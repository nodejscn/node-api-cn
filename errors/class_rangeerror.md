
`Error` 的一个子类，表明一个函数的一个给定的参数的值不在可接受的集合或范围内；
无论是一个数字范围还是给定函数参数的选项的集合。

例子：

```js
require('net').connect(-1);
// 抛出 "RangeError: "port" option should be >= 0 and < 65536: -1"
```

Node.js 会生成并以参数校验的形式立即抛出 `RangeError` 实例。

