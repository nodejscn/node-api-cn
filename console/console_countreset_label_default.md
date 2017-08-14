<!-- YAML
added: v8.3.0
-->

* `label` {string} The display label for the counter. Defaults to `'default'`.

Resets the internal counter specific to `label`.

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

