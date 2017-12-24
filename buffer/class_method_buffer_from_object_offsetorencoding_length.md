<!-- YAML
added: v8.2.0
-->

* `object` {Object} 一个支持 `Symbol.toPrimitive` 或 `valueOf()` 的对象
* `offsetOrEncoding` {number|string} 字节偏移量或编码，取决于 `object.valueOf()` 或 `object[Symbol.toPrimitive]()` 的返回值。
* `length` {number} 长度值，取决于 `object.valueOf()` 或 `object[Symbol.toPrimitive]()` 的返回值。

那些其 `valueOf()` 方法返回值如果不严格等于 `object` 的对象，返回`Buffer.from(object.valueOf(), offsetOrEncoding, length)`。

例子:

```js
const buf = Buffer.from(new String('this is a test'));
// <Buffer 74 68 69 73 20 69 73 20 61 20 74 65 73 74>
```

那些支持 `Symbol.toPrimitive` 的对象， 返回 `Buffer.from(object[Symbol.toPrimitive](), offsetOrEncoding, length)`。

例子:

```js
class Foo {
  [Symbol.toPrimitive]() {
    return 'this is a test';
  }
}

const buf = Buffer.from(new Foo(), 'utf8');
// <Buffer 74 68 69 73 20 69 73 20 61 20 74 65 73 74>
```

