<!-- YAML
added: v0.1.21
changes:
  - version: v10.2.0
    pr-url: https://github.com/nodejs/node/pull/20485
    description: The `error` parameter can be an object containing regular
                 expressions now.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17584
    description: The `error` parameter can now be an object as well.
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3276
    description: The `error` parameter can now be an arrow function.
-->
* `fn` {Function}
* `error` {RegExp|Function|Object|Error}
* `message` {string|Error}

断言 `fn` 函数会抛出错误。

`error` 可以是 [`Class`]、[`RegExp`]、校验函数、每个属性都会被测试是否深度全等的校验对象、或每个属性（包括不可枚举的 `message` 和 `name` 属性）都会被测试是否深度全等的错误实例。
当使用对象时，可以使用正则表达式来校验字符串属性。
详见下面的例子。

如果指定了 `message` 参数，则当 `fn` 函数不抛出错误时，`message` 参数会作为 `AssertionError` 的错误信息。

例子，`error` 参数为自定义的校验对象或错误实例：

```js
const err = new TypeError('错误信息');
err.code = 404;
err.foo = 'bar';
err.info = {
  nested: true,
  baz: 'text'
};
err.reg = /abc/i;

assert.throws(
  () => {
    throw err;
  },
  {
    name: 'TypeError',
    message: '错误信息'
    info: {
      nested: true,
      baz: 'text'
    }
    // 只有校验对象的属性会被测试。
    // 使用嵌套的对象必须提供全部属性，否则校验会失败。 
  }
);

// 使用正则表达式来校验错误属性：
assert.throws(
  () => {
    throw err;
  },
  {
    // `name` 和 `message` 属性为字符串，对它们使用正则表达式进行匹配。
    // 如果校验失败，则抛出错误。
    name: /^TypeError$/,
    message: /错误信息/,
    foo: 'bar',
    info: {
      nested: true,
      // 嵌套的属性不可以使用正则表达式！
      baz: 'text'
    },
    // `reg` 属性包含了一个正则表达式，只有校验对象也包含一个完全相同的正则表达式时，校验才会通过。
    reg: /abc/i
  }
);

// 失败，因为 `message` 属性与 `name` 属性不同：
assert.throws(
  () => {
    const otherErr = new Error('未找到');
    otherErr.code = 404;
    throw otherErr;
  },
  err // 会测试 `message`、`name` 和 `code`。
);
```

例子，`error` 参数为构造函数：

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  Error
);
```

例子，`error` 参数为 [`RegExp`]：

使用正则表达式运行错误对象的 `.toString`， 且包括错误的名称。

```js
assert.throws(
  () => {
    throw new Error('错误信息');
  },
  /^Error: 错误信息$/
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

`error` 不能是字符串。
如果第二个参数是字符串，则视为不传入 `error`，且字符串会用于 `message`。
这可能会造成误解。
使用与抛出的错误信息相同的信息，会导致 `ERR_AMBIGUOUS_ARGUMENT` 错误。
如果需要使用字符串作为第二个参数，请仔细阅读下面的例子。

<!-- eslint-disable no-restricted-syntax -->
```js
function throwingFirst() {
  throw new Error('错误一');
}
function throwingSecond() {
  throw new Error('错误二');
}
function notThrowing() {}

// 第二个参数为字符串，且输入函数抛出了错误。
// 第一个例子不会抛出错误，因为它没有匹配到输入函数抛出的错误信息！
assert.throws(throwingFirst, '错误二');
// 第二个例子中，传入的信息接近错误信息，
// 且没有表述清楚用户是否有意匹配错误信息，
// 所以 Node.js 会抛出 `ERR_AMBIGUOUS_ARGUMENT` 错误。
assert.throws(throwingSecond, '错误二');
// 抛出错误：
// TypeError [ERR_AMBIGUOUS_ARGUMENT]

// 当函数没有抛出错误时，字符串可用于错误信息：
assert.throws(notThrowing, '错误二');
// 抛出 AssertionError [ERR_ASSERTION]: Missing expected exception: 错误二

// 如果想要匹配到错误信息，可以如下：
assert.throws(throwingSecond, /错误二$/);
// 没有抛出错误，因为错误信息匹配。
assert.throws(throwingFirst, /错误二$/);
// 抛出错误：
// Error: 错误一
//     at throwingFirst (repl:2:9)
```

鉴于会混淆语句，建议不要使用字符串作为第二个参数。
这可能会导致不易定位的错误。

