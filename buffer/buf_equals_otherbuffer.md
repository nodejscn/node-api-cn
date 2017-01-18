<!-- YAML
added: v0.11.13
-->

* `otherBuffer` {Buffer} 要比较的 `Buffer`
* 返回: {Boolean}

如果 `buf` 与 `otherBuffer` 具有完全相同的字节，则返回 `true`，否则返回 `false`。

例子：

```js
const buf1 = Buffer.from('ABC');
const buf2 = Buffer.from('414243', 'hex');
const buf3 = Buffer.from('ABCD');

// 输出: true
console.log(buf1.equals(buf2));

// 输出: false
console.log(buf1.equals(buf3));
```

