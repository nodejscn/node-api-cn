<!-- YAML
added: v8.3.0
-->

* `label` {string} 计数器的显示标签。 默认为 `'default'`。

维护一个指定 `label` 的内部计数器并且输出到 `stdout` 指定 `label` 调用 `console.count()` 的次数。

<!-- eslint-skip -->
```js
> console.count()
default: 1
undefined
> console.count('default')
default: 2
undefined
> console.count('abc')
abc: 1
undefined
> console.count('xyz')
xyz: 1
undefined
> console.count('abc')
abc: 2
undefined
> console.count()
default: 3
undefined
>
```

