<!-- YAML
added: v0.3.0
changes:
  - version: v7.1.0, v6.9.2
    pr-url: https://github.com/nodejs/node/pull/9341
    description: Coercing the offsets to integers now handles values outside
                 the 32-bit integer range properly.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/9101
    description: All offsets are now coerced to integers before doing any
                 calculations with them.
-->

* `start` {integer} 新建的 `Buffer` 开始的位置。 **默认:** `0`
* `end` {integer} 新建的 `Buffer` 结束的位置（不包含）。
  **默认:** [`buf.length`]
* 返回: {Buffer}

返回一个指向相同原始内存的新建的 `Buffer`，但做了偏移且通过 `start` 和 `end` 索引进行裁剪。

Specifying `end` greater than [`buf.length`] will return the same result as
that of `end` equal to [`buf.length`].

**注意，修改这个新建的 `Buffer` 切片，也会同时修改原始的 `Buffer` 的内存，因为这两个对象所分配的内存是重叠的。**

例子：创建一个包含 ASCII 字母表的 `Buffer`，并进行切片，然后修改原始 `Buffer` 上的一个字节。

```js
const buf1 = Buffer.allocUnsafe(26);

for (let i = 0; i < 26; i++) {
  // 97 是 'a' 的十进制 ASCII 值 
  buf1[i] = i + 97;
}

const buf2 = buf1.slice(0, 3);

// 输出: abc
console.log(buf2.toString('ascii', 0, buf2.length));

buf1[0] = 33;

// 输出: !bc
console.log(buf2.toString('ascii', 0, buf2.length));
```

指定负的索引会导致切片的生成是相对于 `buf` 的末尾而不是开头。

例子：

```js
const buf = Buffer.from('buffer');

// 输出: buffe
// (相当于 buf.slice(0, 5))
console.log(buf.slice(-6, -1).toString());

// 输出: buff
// (相当于 buf.slice(0, 4))
console.log(buf.slice(-6, -2).toString());

// 输出: uff
// (相当于 buf.slice(1, 4))
console.log(buf.slice(-5, -2).toString());
```

