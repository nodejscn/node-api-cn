
* 返回: {Iterator}

返回在查询字符串中每一个键值对的ES6迭代器。迭代器的每一个项都是一个JavaScript数组。数组中的第一个项是`name`，第二个项是`value`。

别名：[`urlSearchParams.entries()`][].

```js
const { URLSearchParams } = require('url');
const params = new URLSearchParams('foo=bar&xyz=baz');
for (const [name, value] of params) {
  console.log(name, value);
}
  // 输出:
  // foo bar
  // xyz baz
```

