<!-- YAML
added:
  - v7.5.0
  - v6.13.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18281
    description: 该类现在在全局的对象上是可用的。
-->

`URLSearchParams` API 提供对一个 `URL` 的查询的读写访问。
`URLSearchParams` 类也可以被与以下的四个构造器之一一起单独使用。
`URLSearchParams` 类也是在全局的对象上可用的。

WHATWG `URLSearchParams` 接口和 [`querystring`] 模块具有相似的用途，但是 [`querystring`] 模块的用途更加通用，因为它允许分隔符（`＆` 和 `=`）的自定义。
另一方面，此 API 被纯粹地设计用于 URL 查询字符串。

```js
const myURL = new URL('https://example.org/?abc=123');
console.log(myURL.searchParams.get('abc'));
// 打印 123

myURL.searchParams.append('abc', 'xyz');
console.log(myURL.href);
// 打印 https://example.org/?abc=123&abc=xyz

myURL.searchParams.delete('abc');
myURL.searchParams.set('a', 'b');
console.log(myURL.href);
// 打印 https://example.org/?a=b

const newSearchParams = new URLSearchParams(myURL.searchParams);
// 以上的代码等效于
// const newSearchParams = new URLSearchParams(myURL.search);

newSearchParams.append('a', 'c');
console.log(myURL.href);
// 打印 https://example.org/?a=b
console.log(newSearchParams.toString());
// 打印 a=b&a=c

// newSearchParams.toString() 被隐式地调用。
myURL.search = newSearchParams;
console.log(myURL.href);
// 打印 https://example.org/?a=b&a=c
newSearchParams.delete('a');
console.log(myURL.href);
// 打印 https://example.org/?a=b&a=c
```

