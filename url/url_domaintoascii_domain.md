<!-- YAML
added: v7.4.0
-->

* `domain` {string}
* Returns: {string}

Returns the [Punycode][] ASCII serialization of the `domain`. If `domain` is an
invalid domain, the empty string is returned.

It performs the inverse operation to [`url.domainToUnicode()`][].

```js
const url = require('url');
console.log(url.domainToASCII('español.com'));
  // Prints xn--espaol-zwa.com
console.log(url.domainToASCII('中文.com'));
  // Prints xn--fiq228c.com
console.log(url.domainToASCII('xn--iñvalid.com'));
  // Prints an empty string
```

