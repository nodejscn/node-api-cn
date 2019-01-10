
* 返回: {string}

在`URL`对象上调用`toJSON()`方法将返回序列化的URL。返回值与[`url.href`][]和[`url.toString()`][]的相同。

当`URL`对象使用[`JSON.stringify()`][]序列化时将自动调用该方法。

```js
const { URL } = require('url');
const myURLs = [
  new URL('https://www.example.com'),
  new URL('https://test.example.org')
];
console.log(JSON.stringify(myURLs));
  // 输出 ["https://www.example.com/","https://test.example.org/"]
```

