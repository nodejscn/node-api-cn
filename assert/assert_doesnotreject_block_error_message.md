<!-- YAML
added: v10.0.0
-->
* `block` {Function|Promise}
* `error` {RegExp|Function}
* `message` {string|Error}

等待 `block` 的 promise 完成，如果 `block` 是一个函数，则立即调用该函数并等待返回的 promise 完成，然后检查 promise 是否被 reject。

如果 `block` 是一个函数且同步地抛出一个错误，则 `assert.doesNotReject()` 会返回一个被 reject 的 `Promise` 并传入该错误。
如果该函数没有返回一个 promise，则 `assert.doesNotReject()` 会返回一个被 reject 的 `Promise` 并传入 [`ERR_INVALID_RETURN_VALUE`] 错误。
以上两种情况都会跳过错误处理函数。

`error` 可以是 [`Class`]、[`RegExp`] 或校验函数。
详见 [`assert.throws()`]。

该函数相当于 [`assert.doesNotThrow()`]，除了需要等待完成的异步特性。

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

