<!-- YAML
added: v0.1.21
-->

期望 `block` 函数抛出错误。

如果指定 `error`，它可以是一个构造函数、[正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)、或校验函数。

如果指定 `message`，当 `block` 函数抛出错误时，`message` 会作为错误信息传给 `AssertionError`。

使用构造函数的例子：

```js
assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  Error
);
```

使用正则表达式的例子：

```js
assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  /value/
);
```

使用自定义校验函数的例子：

```js
assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  function(err) {
    if ( (err instanceof Error) && /value/.test(err) ) {
      return true;
    }
  },
  'unexpected error'
);
```

注意，`error` 参数不能是字符串。
如果第二个参数是字符串，则视为不传 `error` 参数，传入的字符串会被当作是 `message` 的值。
这可能会引起误解：

```js
// 这是错误的！不要这么做！
assert.throws(myFunction, 'missing foo', 'did not throw with expected message');

// 应该这么做。
assert.throws(myFunction, /missing foo/, 'did not throw with expected message');
```

