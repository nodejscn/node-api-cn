<!-- YAML
added: v0.1.21
changes:
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3276
    description: The `error` parameter can now be an arrow function.
-->
* `block` {Function}
* `error` {RegExp|Function}
* `message` {any}

期望 `block` 函数抛出错误。

如果指定了 `error`，`error` 可以是构造函数、[正则表达式]、或自定义的验证函数。

如果指定了 `message`，则当 `block` 不抛出错误时，`message` 会作为 `AssertionError` 的错误信息。

例子，使用构造函数验证实例：

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  Error
);
```

例子，使用 [正则表达式] 验证错误信息：

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  /错误/
);
```

例子，自定义的错误验证函数：

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  function(err) {
    if ((err instanceof Error) && /错误/.test(err)) {
      return true;
    }
  },
  '不是期望的错误'
);
```

注意，`error` 不能是一个字符串。
如果第二个参数是一个字符串，则视为省略 `error` 参数，传入的字符串会被用于 `message`。
这点比较容易搞错：

<!-- eslint-disable assert-throws-arguments -->
```js
// 这是错误的！不要这么做！
assert.throws(myFunction, '错误', '没有抛出期望的信息');

// 应该这么做。
assert.throws(myFunction, /错误/, '没有抛出期望的信息');
```

