<!-- YAML
added: v7.4.0
-->

* `domain` {string}
* 返回: {string}

返回Unicode序列化的`domain`. 如果`domain`是无效域名，将返回空字符串。

它执行的是[`url.domainToASCII()`][]的逆运算。

```js
const url = require('url');
console.log(url.domainToUnicode('xn--espaol-zwa.com'));
  // 输出 español.com
console.log(url.domainToUnicode('xn--fiq228c.com'));
  // 输出 中文.com
console.log(url.domainToUnicode('xn--iñvalid.com'));
  // 输出空字符串
```

