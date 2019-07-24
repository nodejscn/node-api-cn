<!-- YAML
added: v7.6.0
-->

* `URL` {URL} 一个[WHATWG URL][]对象
* `options` {Object}
  * `auth` {boolean} 如果序列化的URL字符串应该包含用户名和密码为`true`，否则为`false`。默认为`true`。
  * `fragment` {boolean} 如果序列化的URL字符串应该包含分段为`true`，否则为`false`。默认为`true`。
  * `search` {boolean} 如果序列化的URL字符串应该包含搜索查询为`true`，否则为`false`。默认为`true`。
  * `unicode` {boolean} `true` 如果出现在URL字符串主机元素里的Unicode字符应该被直接编码而不是使用Punycode编码为`true`，默认为`false`。

返回一个[WHATWG URL][]对象的可自定义序列化的URL字符串表达。

虽然URL对象的`toString()`方法和`href`属性都可以返回URL的序列化的字符串。然而，两者都不可以被自定义。而`url.format(URL[, options])`方法允许输出的基本自定义。

例如：

```js
const { URL } = require('url');
const myURL = new URL('https://a:b@你好你好?abc#foo');

console.log(myURL.href);
  // 输出 https://a:b@xn--6qqa088eba/?abc#foo

console.log(myURL.toString());
  // 输出 https://a:b@xn--6qqa088eba/?abc#foo

console.log(url.format(myURL, { fragment: false, unicode: true, auth: false }));
  // 输出 'https://你好你好/?abc'
```

