<!-- YAML
added: v8.3.0
-->

* `label` {string} 计数器的显示标签。 **默认值:** `'default'`。

重置特定于 `label` 的内部计数器。

<!-- eslint-skip -->
```js
> console.count('abc');
abc: 1
undefined
> console.countReset('abc');
undefined
> console.count('abc');
abc: 1
undefined
>
```

