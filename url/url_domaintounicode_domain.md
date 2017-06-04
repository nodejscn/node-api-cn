<!-- YAML
added: v7.4.0
-->

* `domain` {string}
* Returns: {string}

Returns the Unicode serialization of the `domain`. If `domain` is an invalid
domain, the empty string is returned.

It performs the inverse operation to [`url.domainToASCII()`][].

```js
const url = require('url');
console.log(url.domainToUnicode('xn--espaol-zwa.com'));
  // Prints español.com
console.log(url.domainToUnicode('xn--fiq228c.com'));
  // Prints 中文.com
console.log(url.domainToUnicode('xn--iñvalid.com'));
  // Prints an empty string
```

