<!-- YAML
added: v10.0.0
-->
* `asyncFn` {Function|Promise}
* `error` {RegExp|Function}
* `message` {string}

等待 `asyncFn` 的 Promise，如果 `asyncFn` 是函数，则立即调用并等待返回的 Promise 完成，然后检查 Promise 是否被 reject。

如果 `asyncFn` 是函数且同步地抛出错误，则 `assert.doesNotReject()` 会返回被 reject 的 `Promise` 并带上错误对象。
如果 `asyncFn` 函数没有返回 Promise，则 `assert.doesNotReject()` 会返回被 reject 的 `Promise` 并带上 [`ERR_INVALID_RETURN_VALUE`] 错误。
以上两种情况都会跳过错误处理函数。

`assert.doesNotReject()` 并不常用，因为很少需要捕获一个被 reject 的 Promise 然后再次 reject。

`error` 可以是 [`Class`]、[`RegExp`] 或校验函数。
详见 [`assert.throws()`]。

与 [`assert.doesNotThrow()`] 的区别在于需要异步地等待完成。


```js
(async () => {
  await assert.doesNotReject(
    async () => {
      throw new TypeError('错误信息');
    },
    SyntaxError
  );
})();
```

```js
assert.doesNotReject(Promise.reject(new TypeError('错误信息')))
  .then(() => {
    // ...
  });
```

