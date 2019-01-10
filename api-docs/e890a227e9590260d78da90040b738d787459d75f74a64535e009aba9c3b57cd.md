<!-- YAML
added: v7.10.0
-->

* `obj` {Object} 一个表示键值对集合的对象

通过使用查询哈希映射实例化一个新的`URLSearchParams`对象，`obj`的每一个属性的键和值将被强制转换为字符串。

*请注意*: 和 [`querystring`][] 模块不同的是, 在数组的形式中，重复的键是不允许的。数组使用[`array.toString()`][]进行字符串化时，只需用逗号连接所有的数组元素即可。

```js
const { URLSearchParams } = require('url');
const params = new URLSearchParams({
  user: 'abc',
  query: ['first', 'second']
});
console.log(params.getAll('query'));
  // 输出 [ 'first,second' ]
console.log(params.toString());
  // 输出 'user=abc&query=first%2Csecond'
```

