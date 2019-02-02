<!-- YAML
added: v0.1.21
changes:
  - version: v5.11.0, v4.4.5
    pr-url: https://github.com/nodejs/node/pull/2407
    description: The `message` parameter is respected now.
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3276
    description: The `error` parameter can now be an arrow function.
-->
* `fn` {Function}
* `error` {RegExp|Function}
* `message` {string}

断言 `fn` 函数不会抛出错误。

使用 `assert.doesNotThrow()` 实际上没有用处，因为捕获错误然后重新抛出它没有任何好处。
应该考虑在不应抛出错误的特定代码路径旁边添加注释，并尽可能保留错误消息。

当调用 `assert.doesNotThrow()` 时，它将立即调用 `fn` 函数。

如果抛出错误并且它与 `error` 参数指定的类型相同，则抛出 `AssertionError`。
如果错误的类型不同，或者 `error` 参数未定义，则错误将传播回调用方。

如果指定，则 `error` 可以是 [`Class`]、[`RegExp`] 或验证函数。
有关更多详细信息，请参见 [`assert.throws()`]。

例如，以下示例将抛出 [`TypeError`]，因为断言中没有匹配的错误类型：


<!-- eslint-disable no-restricted-syntax -->
```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误值');
  },
  SyntaxError
);
```

以下示例将导致 `AssertionError`，并显示消息 'Got unwanted exception...'：

<!-- eslint-disable no-restricted-syntax -->
```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误值');
  },
  TypeError
);
```

如果抛出 `AssertionError` 并为 `message` 参数提供了值，则 `message` 的值将附加到 `AssertionError` 消息：

<!-- eslint-disable no-restricted-syntax -->
```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误值');
  },
  /错误值/,
  '出错啦'
);
// AssertionError: Got unwanted exception: 出错啦
```

