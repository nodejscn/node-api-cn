<!-- YAML
added:
  - v7.10.0
  - v6.13.0
-->

* `iterable` {Iterable} 元素是键值对的迭代对象。

以一种类似于 [`Map`] 的构造函数的迭代映射方式实例化一个新的 `URLSearchParams` 对象。
`iterable` 可以是一个 `Array` 或者任何迭代对象。
这就意味着 `iterable` 能够是另一个 `URLSearchParams`，这种情况下，构造函数将简单地根据提供的 `URLSearchParams` 创建一个克隆 `URLSearchParams`。
`iterable` 的元素是键值对，并且其本身也可以是任何迭代对象。

允许重复的键。

```js
let params;

// 使用数组。
params = new URLSearchParams([
  ['user', 'abc'],
  ['query', 'first'],
  ['query', 'second']
]);
console.log(params.toString());
// 打印 'user=abc&query=first&query=second'

// 使用 Map 对象。
const map = new Map();
map.set('user', 'abc');
map.set('query', 'xyz');
params = new URLSearchParams(map);
console.log(params.toString());
// 打印 'user=abc&query=xyz'

// 使用 generator 函数。
function* getQueryPairs() {
  yield ['user', 'abc'];
  yield ['query', 'first'];
  yield ['query', 'second'];
}
params = new URLSearchParams(getQueryPairs());
console.log(params.toString());
// 打印 'user=abc&query=first&query=second'

// 每个键值对必须有两个元素。
new URLSearchParams([
  ['user', 'abc', 'error']
]);
// 抛出 TypeError [ERR_INVALID_TUPLE]:
//        Each query pair must be an iterable [name, value] tuple
```

