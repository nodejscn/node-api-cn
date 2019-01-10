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

`assert.doesNotThrow()` 并不常用，因为很少需要捕获一个错误然后再次抛出错误。

当 `assert.doesNotThrow()` 被调用时，会立即调用 `fn` 函数。

如果抛出错误，且错误与 `error` 参数指定的类型相同，则抛出 `AssertionError`。
如果错误类型不同，或 `error` 参数为 `undefined`，则错误会冒泡给调用者。

`error` 可以是 [`Class`]、[`RegExp`] 或校验函数。
详见 [`assert.throws()`]。


以下例子会抛出 [`TypeError`]，因为断言没有匹配错误的类型：

<!-- eslint-disable no-restricted-syntax -->
```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误信息');
  },
  SyntaxError
);
```

以下例子会抛出 `AssertionError`，并带上 'Got unwanted exception...' 信息：

<!-- eslint-disable no-restricted-syntax -->
```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误信息');
  },
  TypeError
);
```

如果抛出 `AssertionError` 且为 `message` 参数传了值，则 `message` 的值会附加到 `AssertionError` 消息：

<!-- eslint-disable no-restricted-syntax -->
```js
assert.doesNotThrow(
  () => {
    throw new TypeError('错误信息');
  },
  /错误信息/,
  '出错啦'
);
// 抛出: AssertionError: Got unwanted exception: 出错啦
```

