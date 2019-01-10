<!-- YAML
added: v0.6.1
-->

* `domain` {string}

The `punycode.toASCII()` method converts a Unicode string representing an
Internationalized Domain Name to [Punycode][]. Only the non-ASCII parts of the
domain name will be converted. Calling `punycode.toASCII()` on a string that
already only contains ASCII characters will have no effect.

```js
// encode domain names
punycode.toASCII('mañana.com');  // 'xn--maana-pta.com'
punycode.toASCII('☃-⌘.com');   // 'xn----dqo34k.com'
punycode.toASCII('example.com'); // 'example.com'
```

