<!-- YAML
added: v10.0.0
-->
* `asyncFn` {Function|Promise}
* `error` {RegExp|Function|Object|Error}
* `message` {string}

等待 `asyncFn` Promise，或者，如果 `asyncFn` 是一个函数，则立即调用该函数并等待返回的 Promise 完成。
然后它将检查 Promise 是否被拒绝。

如果 `asyncFn` 是一个函数并且它同步抛出一个错误，则 `assert.rejects()` 将返回一个带有该错误的被拒绝的 `Promise`。
如果函数未返回 Promise，则 `assert.rejects()` 将返回一个被拒绝的 `Promise`，其中包含 [`ERR_INVALID_RETURN_VALUE`] 错误。
在这两种情况下都会跳过错误处理函数。

除了等待的异步性质之外，完成行为与 [`assert.throws()`] 完全相同。

如果指定，则 `error` 可以是 [`Class`]、[`RegExp`]、验证函数、将测试每个属性的对象、或者将测试每个属性的错误实例（包括不可枚举的 `message` 和 `name` 属性）。

如果指定 `message`，则当 `asyncFn` 无法拒绝时 `message` 将是 `AssertionError` 提供的消息。

```js
(async () => {
  await assert.rejects(
    async () => {
      throw new TypeError('错误值');
    },
    {
      name: 'TypeError',
      message: '错误值'
    }
  );
})();
```

```js
assert.rejects(
  Promise.reject(new Error('错误值')),
  Error
).then(() => {
  // ...
});
```

注意，`error` 不能是字符串。
如果提供了一个字符串作为第二个参数，则假定 `error` 被忽略，而字符串将用于 `message`。
这可能导致容易错过的错误。
如果考虑使用字符串作为第二个参数，请仔细阅读 [`assert.throws()`] 中的示例。

