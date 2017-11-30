<!-- YAML
added: v1.6.0
-->

* `name` {string}
* `value` {string}

为 headers 对象设置一个单一的 header 值。如果该 header 已经存在了，则将会被替换。这里使用一个字符串数组来设置有相同名称的多个 headers。

例如：
```js
request.setHeader('Content-Type', 'application/json');
```

或

```js
request.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
```

