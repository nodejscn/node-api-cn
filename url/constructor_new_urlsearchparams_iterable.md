<!-- YAML
added: v7.10.0
-->

* `iterable` {Iterable} 一个元素时键值对的迭代对象

以一种类似于[`Map`][]的构造函数的迭代映射方式实例化一个新的`URLSearchParams`对象。`iterable`可以是一个数组或者任何迭代对象。这就意味着`iterable`能够使另一个`URLSearchParams`，这种情况下，构造函数将简单地根据提供的`URLSearchParams`创建一个克隆`URLSearchParams`。`iterable`的元素是键值对，并且其本身也可以是任何迭代对象。

允许重复的键。

```js
const { URLSearchParams } = require('url');
let params;

// Using an array
params = new URLSearchParams([
  ['user', 'abc'],
  ['query', 'first'],
  ['query', 'second']
]);
console.log(params.toString());
  // 输出 'user=abc&query=first&query=second'

// 使用Map对象
const map = new Map();
map.set('user', 'abc');
map.set('query', 'xyz');
params = new URLSearchParams(map);
console.log(params.toString());
  // 输出 'user=abc&query=xyz'

// 使用generator函数
function* getQueryPairs() {
  yield ['user', 'abc'];
  yield ['query', 'first'];
  yield ['query', 'second'];
}
params = new URLSearchParams(getQueryPairs());
console.log(params.toString());
  // 输出 'user=abc&query=first&query=second'

// 每个键值对必须有两个元素
new URLSearchParams([
  ['user', 'abc', 'error']
]);
  // 抛出 TypeError [ERR_INVALID_TUPLE]:
  //        每一个键值对必须是迭代的[键，值]元组
```

