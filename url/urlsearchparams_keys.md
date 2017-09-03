
* 返回: {Iterator}

在每一个键值对上返回一个键的ES6迭代器。

```js
const { URLSearchParams } = require('url');
const params = new URLSearchParams('foo=bar&foo=baz');
for (const name of params.keys()) {
  console.log(name);
}
  // 输出:
  // foo
  // foo
```

