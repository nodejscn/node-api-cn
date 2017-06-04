<!-- YAML
added: v0.1.101
-->
* `value` {any}
* `message` {any}
* `...args` {any}

一个简单的断言测试，验证 `value` 是否为真。
如果不为真，则抛出 `AssertionError`。
如果提供了 `message`，则使用 [`util.format()`] 格式化并作为错误信息使用。

```js
console.assert(true, 'does nothing');
// 通过
console.assert(false, 'Whoops %s', 'didn\'t work');
// AssertionError: Whoops didn't work
```

注意：Node.js 中的 `console.assert()` 方法与[在浏览器中]的 `console.assert()` 方法的实现是不一样的。

具体地说，在浏览器中，用非真的断言调用 `console.assert()` 会导致 `message` 被打印到控制台但不会中断后续代码的执行。
而在 Node.js 中，非真的断言会导致抛出 `AssertionError`。

可以通过扩展 Node.js 的 `console` 并重写 `console.assert()` 方法来实现与浏览器中类似的功能。

例子，创建一个简单的模块，并扩展与重写了 Node.js 中 `console` 的默认行为。

<!-- eslint-disable func-name-matching -->
```js
'use strict';

// 用一个新的不带补丁的 assert 实现来创建一个简单的 console 扩展。
const myConsole = Object.create(console, {
  assert: {
    value: function assert(assertion, message, ...args) {
      try {
        console.assert(assertion, message, ...args);
      } catch (err) {
        console.error(err.stack);
      }
    },
    configurable: true,
    enumerable: true,
    writable: true,
  },
});

module.exports = myConsole;
```

然后可以用来直接替换内置的 console：

```js
const console = require('./myConsole');
console.assert(false, '会打印这个消息，但不会抛出错误');
console.log('这个也会打印');
```

