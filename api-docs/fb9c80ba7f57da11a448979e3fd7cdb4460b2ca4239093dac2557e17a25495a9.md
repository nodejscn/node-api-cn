
* `fn` {Function} 在查询字符串中的每个键值对的调用函数。
* `thisArg` {Object} 当`fn`调用时，被用作`this`值的对象

在查询字符串中迭代每个键值对，并调用给定的函数。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/?a=b&c=d');
myURL.searchParams.forEach((value, name, searchParams) => {
  console.log(name, value, myURL.searchParams === searchParams);
});
  // 输出:
  // a b true
  // c d true
```

