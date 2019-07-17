<!-- YAML
added: v3.0.0
-->

* `start` {integer} 新 `Buffer` 开始的位置。**默认值:** `0`。
* `end` {integer} 新 `Buffer` 结束的位置（不包含）。**默认值:** [`buf.length`]。
* 返回: {Buffer}

返回一个新的 `Buffer`，它引用与原始的 Buffer 相同的内存，但是由 `start` 和 `end` 索引进行偏移和裁剪。

指定大于 [`buf.length`] 的 `end` 将会返回与 `end` 等于 [`buf.length`] 时相同的结果。

修改新的 `Buffer` 切片将会修改原始 `Buffer` 中的内存，因为两个对象分配的内存是重叠的。

```js
// 使用 ASCII 字母创建一个 `Buffer`，然后进行切片，再修改原始 `Buffer` 中的一个字节。

const buf1 = Buffer.allocUnsafe(26);

for (let i = 0; i < 26; i++) {
  // 97 是 'a' 的十进制 ASCII 值。
  buf1[i] = i + 97;
}

const buf2 = buf1.subarray(0, 3);

console.log(buf2.toString('ascii', 0, buf2.length));
// 打印: abc

buf1[0] = 33;

console.log(buf2.toString('ascii', 0, buf2.length));
// 打印: !bc
```

指定负的索引会导致切片的生成是相对于 `buf` 的末尾而不是开头。

```js
const buf = Buffer.from('buffer');

console.log(buf.subarray(-6, -1).toString());
// 打印: buffe
// (相当于 buf.subarray(0, 5)。)

console.log(buf.subarray(-6, -2).toString());
// 打印: buff
// (相当于 buf.subarray(0, 4)。)

console.log(buf.subarray(-5, -2).toString());
// 打印: uff
// (相当于 buf.subarray(1, 4)。)
```

