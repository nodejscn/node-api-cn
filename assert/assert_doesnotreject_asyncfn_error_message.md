<!-- YAML
added: v10.0.0
-->
* `asyncFn` {Function|Promise}
* `error` {RegExp|Function}
* `message` {string}

等待 `asyncFn` Promise，或者，如果 `asyncFn` 是一个函数，则立即调用该函数并等待返回的 Promise 完成。
然后它将检查 Promise 是否被拒绝。

如果 `asyncFn` 是一个函数并且它同步抛出一个错误，则 `assert.doesNotReject()` 将返回一个带有该错误的被拒绝的 `Promise`。
如果函数未返回 Promise，则 `assert.doesNotReject()` 将返回一个被拒绝的 `Promise`，其中包含 [`ERR_INVALID_RETURN_VALUE`] 错误。
在这两种情况下都会跳过错误处理函数。

使用 `assert.doesNotReject()` 实际上没有用处，因为捕获拒绝然后再次拒绝它几乎没有什么好处。
应该考虑在不应拒绝的特定代码路径旁边添加注释，并尽可能保留错误消息。

如果指定，则 `error` 可以是 [`Class`]、[`RegExp`] 或验证函数。
有关更多详细信息，请参见 [`assert.throws()`]。

除了等待的异步性质之外，完成行为与 [`assert.doesNotThrow()`] 完全相同。


```js
(async () => {
  await assert.doesNotReject(
    async () => {
      throw new TypeError('错误值');
    },
    SyntaxError
  );
})();
```

```js
assert.doesNotReject(Promise.reject(new TypeError('错误值')))
  .then(() => {
    // ...
  });
```

