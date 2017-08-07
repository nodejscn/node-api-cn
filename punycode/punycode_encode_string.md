<!-- YAML
added: v0.5.1
-->

* `string` {string}

`punycode.encode()`方法将一个Unicode编码的字符串转化为等价的只含有ASCII字符的[Punycode][]字符串。

```js
punycode.encode('mañana'); // 'maana-pta'
punycode.encode('☃-⌘'); // '--dqo34k'
```

