
* {URLSearchParams}

获取表示 URL 的查询参数的 [`URLSearchParams`] 对象。
此属性是只读的，但是它提供的 `URLSearchParams` 对象可以被用于改变 URL 实例。
要替换 URL 的整个查询参数，则使用 [`url.search`] 设置器。
查看 [`URLSearchParams`] 文档获取详情。

使用 `.searchParams` 修改 `URL` 时要谨慎，因为按照 WHATWG 规范，`URLSearchParams` 对象使用不同的规则来判断要百分比编码的字符。
例如，`URL` 对象不会百分比编码 ASCII 波浪号（`〜`），而 `URLSearchParams` 始终会编码它：

```js
const myUrl = new URL('https://example.org/abc?foo=~bar');

console.log(myUrl.search);  // 打印 ?foo=~bar

// 通过 searchParams 修改 URL
myUrl.searchParams.sort();

console.log(myUrl.search);  // 打印 ?foo=%7Ebar
```

