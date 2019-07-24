
* `name` {string}
* `value` {string}

将`URLSearchParams`对象中与`name`相对应的值设置为`value`。如果已经存在键为`name`的键值对，将第一对的值设为`value`并且删除其他对。如果不存在，则将此键值对附加在查询字符串后。

```js
const { URLSearchParams } = require('url');

const params = new URLSearchParams();
params.append('foo', 'bar');
params.append('foo', 'baz');
params.append('abc', 'def');
console.log(params.toString());
  // 输出 foo=bar&foo=baz&abc=def

params.set('foo', 'def');
params.set('xyz', 'opq');
console.log(params.toString());
  // 输出 foo=def&abc=def&xyz=opq
```

