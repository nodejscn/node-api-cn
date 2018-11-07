<!-- YAML
added: v10.0.0
-->
* `asyncFn` {Function|Promise}
* `error` {RegExp|Function|Object|Error}
* `message` {string}

等待 `asyncFn` 的 Promise，如果 `asyncFn` 是函数，则立即调用并等待返回的 Promise 完成，然后检查 Promise 是否被 reject。

如果 `asyncFn` 是函数且同步地抛出错误，则 `assert.rejects()` 会返回被 reject 的 `Promise` 并带上错误对象。
如果 `asyncFn` 函数没有返回 Promise，则 `assert.rejects()` 会返回被 reject 的 `Promise` 并带上 [`ERR_INVALID_RETURN_VALUE`] 错误。
以上两种情况都会跳过错误处理函数。

与 [`assert.throws()`] 的区别在于需要异步地等待完成。

`error` 可以是 [`Class`]、[`RegExp`]、校验函数、每个属性都会被测试的对象、或每个属性（包括不可枚举的 `message` 和 `name` 属性）都会被测试的错误实例。

如果指定了 `message`，则当 `asyncFn` 没被 reject 时，`message` 参数会作为 `AssertionError` 的错误信息。

```js
(async () => {
  await assert.rejects(
    async () => {
      throw new TypeError('错误信息');
    },
    {
      name: 'TypeError',
      message: '错误信息'
    }
  );
})();
```

```js
assert.rejects(
  Promise.reject(new Error('错误信息')),
  Error
).then(() => {
  // ...
});
```

`error` 不能是字符串。
如果第二个参数是字符串，则视为不传入 `error`，且字符串会用于 `message`。
这可能会造成误解。
如果需要使用字符串作为第二个参数，请仔细阅读 [`assert.throws()`] 中的例子。

