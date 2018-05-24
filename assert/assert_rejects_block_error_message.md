<!-- YAML
added: v10.0.0
-->
* `block` {Function|Promise}
* `error` {RegExp|Function|Object|Error}
* `message` {string|Error}

等待 `block` 的 promise 完成，如果 `block` 是一个函数，则立即调用该函数并等待返回的 promise 完成，然后检查 promise 是否被 reject。

如果 `block` 是一个函数且同步地抛出一个错误，则 `assert.rejects()` 会返回一个被 reject 的 `Promise` 并传入该错误。
如果该函数没有返回一个 promise，则 `assert.rejects()` 会返回一个被 reject 的 `Promise` 并传入 [`ERR_INVALID_RETURN_VALUE`] 错误。
以上两种情况都会跳过错误处理函数。

该函数相当于 [`assert.throws()`]，除了需要等待完成的异步特性。

`error` 可以是 [`Class`]、[`RegExp`]、校验函数、每个属性都会被测试的对象、或每个属性（包括不可枚举的 `message` 和 `name` 属性）都会被测试的错误实例。

如果指定了 `message`，则当 `block` 没被 reject 时，`message` 参数会作为 `AssertionError` 的错误信息。

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

注意，`error` 不能是字符串。
如果第二个参数是字符串，则视为不传入 `error`，且字符串会用于 `message`。
这可能会造成误解。
如果需要使用字符串作为第二个参数，请仔细阅读 [`assert.throws()`] 中的例子。

