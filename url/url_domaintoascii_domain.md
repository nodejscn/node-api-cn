<!-- YAML
added: v7.4.0
-->

* `domain` {string}
* 返回: {string}

返回[Punycode][] ASCII序列化的`domain`. 如果`domain`是无效域名，将返回空字符串。

它执行的是[`url.domainToUnicode()`][]的逆运算。

```js
const url = require('url');
console.log(url.domainToASCII('español.com'));
  // 输出 xn--espaol-zwa.com
console.log(url.domainToASCII('中文.com'));
  // 输出 xn--fiq228c.com
console.log(url.domainToASCII('xn--iñvalid.com'));
  // 输出空字符串
```

