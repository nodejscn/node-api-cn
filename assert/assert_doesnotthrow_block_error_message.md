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
* `block` {Function}
* `error` {RegExp|Function}
* `message` {any}

断言 `block` 函数不会抛出错误。

当 `assert.doesNotThrow()` 被调用时，它会立即调用 `block` 函数。

如果抛出错误且错误类型与 `error` 参数指定的相同，则抛出 `AssertionError`。
如果错误类型不相同，或 `error` 参数为 `undefined`，则抛出错误。

以下例子会抛出 [`TypeError`]，因为在断言中没有匹配的错误类型：

```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误信息');
  },
  SyntaxError
);
```

以下例子会抛出一个带有 `Got unwanted exception (TypeError)..` 信息的 `AssertionError`：

```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误信息');
  },
  TypeError
);
```

如果抛出了 `AssertionError` 且有给 `message` 参数传值，则 `message` 参数的值会被附加到 `AssertionError` 的信息中：

```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误信息');
  },
  TypeError,
  '抛出错误'
);
// 抛出 AssertionError: Got unwanted exception (TypeError). 抛出错误
```

