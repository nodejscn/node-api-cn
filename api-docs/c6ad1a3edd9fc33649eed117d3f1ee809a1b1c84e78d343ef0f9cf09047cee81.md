<!-- YAML
added: v0.5.1
-->

* `string` {string}

The `punycode.encode()` method converts a string of Unicode codepoints to a
[Punycode][] string of ASCII-only characters.

```js
punycode.encode('mañana'); // 'maana-pta'
punycode.encode('☃-⌘'); // '--dqo34k'
```

