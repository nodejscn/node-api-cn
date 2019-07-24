<!-- YAML
added: v0.5.1
-->

* `string` {string}

The `punycode.decode()` method converts a [Punycode][] string of ASCII-only
characters to the equivalent string of Unicode codepoints.

```js
punycode.decode('maana-pta'); // 'mañana'
punycode.decode('--dqo34k'); // '☃-⌘'
```

