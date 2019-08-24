<!-- YAML
added: v7.6.0
-->

* `URL` {URL} [WHATWG URL] 对象。
* `options` {Object}
  * `auth` {boolean} 如果序列化的 URL 字符串应该包含用户名和密码则为 `true`，否则为 `false`。**默认值:** `true`。
  * `fragment` {boolean} 如果序列化的 URL 字符串应该包含分段则为 `true`，否则为 `false`。**默认值:** `true`。
  * `search` {boolean} 如果序列化的 URL 字符串应该包含搜索查询则为 `true`，否则为 `false`。**默认值:** `true`。
  * `unicode` {boolean} 如果出现在 URL 字符串主机元素里的 Unicode 字符应该被直接编码而不是使用 Punycode 编码则为 `true`。**默认值:** `false`。
* 返回: {string}

返回代表 [WHATWG URL] 对象的可自定义序列化的 URL `String`。

虽然 URL 对象的 `toString()` 方法和 `href` 属性都可以返回 URL 的序列化的字符串。
然而，两者都不可以被自定义。
而 `url.format(URL[, options])` 方法允许输出的基本自定义。



```js
const myURL = new URL('https://a:b@測試?abc#foo');

console.log(myURL.href);
// 打印 https://a:b@xn--g6w251d/?abc#foo

console.log(myURL.toString());
// 打印 https://a:b@xn--g6w251d/?abc#foo

console.log(url.format(myURL, { fragment: false, unicode: true, auth: false }));
// 打印 'https://測試/?abc'
```

