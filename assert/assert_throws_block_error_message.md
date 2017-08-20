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

断言 `block` 函数会抛出错误。

`error` 参数可以是构造函数、[正则表达式]、或自定义函数。

如果指定了 `message` 参数，则当 `block` 函数不抛出错误时，`message` 参数会作为 `AssertionError` 的错误信息。

例子，`error` 参数为构造函数：

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  Error
);
```

例子，`error` 参数为正则表达式：

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  /错误/
);
```

例子，`error` 参数为自定义函数：

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

`error` 参数不能是字符串。
如果第二个参数是字符串，则视为省略 `error` 参数，传入的字符串会被用于 `message` 参数。
例如：

<!-- eslint-disable no-restricted-syntax -->
```js
// 这是错误的！不要这么做！
assert.throws(myFunction, '错误信息', '没有抛出期望的信息');

// 应该这么做。
assert.throws(myFunction, /错误信息/, '没有抛出期望的信息');
```

