<!-- YAML
added: v0.6.1
-->

* `domain` {string}

The `punycode.toUnicode()` method converts a string representing a domain name
containing [Punycode][] encoded characters into Unicode. Only the [Punycode][]
encoded parts of the domain name are be converted.

```js
// decode domain names
punycode.toUnicode('xn--maana-pta.com'); // 'mañana.com'
punycode.toUnicode('xn----dqo34k.com');  // '☃-⌘.com'
punycode.toUnicode('example.com');       // 'example.com'
```

