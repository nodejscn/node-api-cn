<!-- YAML
added: v0.1.21
-->

断言 `block` 函数不会抛出错误。
查看 [assert.throws()](#assert_assert_throws_block_error_message) 了解更多。

当调用 `assert.doesNotThrow()` 时，它会立即调用 `block` 函数。

如果 `block` 函数抛出错误，并且错误类型与 `error` 参数指定的相同，则抛出 `AssertionError`。
如果错误类型不相同，或 `error` 参数是 `undefined`，则错误回传给调用者。

以下例子会抛出 [TypeError](errors.html#errors_class_typeerror)，因为在断言中没有匹配的错误类型：

```js
assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  SyntaxError
);
```

以下例子会抛出一个带有 'Got unwanted exception (TypeError)..' 信息的 `AssertionError`：

```js
assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  TypeError
);
```

如果抛出了 `AssertionError`，并且有为 `message` 参数传值，则 `message` 的值会被追加到 `AssertionError` 的消息中：

```js
assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  TypeError,
  'Whoops'
);
// 抛出 AssertionError: Got unwanted exception (TypeError). Whoops
```

