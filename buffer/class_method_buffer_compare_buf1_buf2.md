<!-- YAML
added: v0.11.13
-->

* `buf1` {Buffer}
* `buf2` {Buffer}
* Returns: {Integer}

比较 `buf1` 和 `buf2` ，通常用于 `Buffer` 实例数组的排序。
相当于调用 [`buf1.compare(buf2)`] 。

例子：

```js
const buf1 = Buffer.from('1234');
const buf2 = Buffer.from('0123');
const arr = [buf1, buf2];

// 输出: [ <Buffer 30 31 32 33>, <Buffer 31 32 33 34> ]
// (结果相当于: [buf2, buf1])
console.log(arr.sort(Buffer.compare));
```

