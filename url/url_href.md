
* {string}

获取及设置序列化的URL。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/foo');
console.log(myURL.href);
  // 输出 https://example.org/foo

myURL.href = 'https://example.com/bar';
console.log(myURL.href);
  // 输出 https://example.com/bar
```

获取`href`属性的值等同于调用[`url.toString()`][]。

将此属性的值设置为新值等同于[`new URL(value)`][`new URL()`]使用创建新的`URL`对象。`URL`对象的每个属性都将被修改。

如果给`href`属性设置的值是无效URL，将会抛出`TypeError`。

