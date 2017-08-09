<!-- YAML
added: v0.1.90
-->

* `encoding` {string} 解码使用的字符编码。**默认:** `'utf8'`
* `start` {integer} 开始解码的字节偏移量。**默认:** `0`
* `end` {integer} 结束解码的字节偏移量（不包含）。
  **默认:** [`buf.length`]
* 返回: {string}

根据 `encoding` 指定的字符编码解码 `buf` 成一个字符串。
`start` 和 `end` 可传入用于只解码 `buf` 的一部分。

字符串实例的最大长度（以UTF-16代码为单位）可查看[`buffer.constants.MAX_STRING_LENGTH`][]。

例子：

```js
const buf1 = Buffer.allocUnsafe(26);

for (let i = 0; i < 26; i++) {
  // 97 是 'a' 的十进制 ASCII 值
  buf1[i] = i + 97;
}

// 输出: abcdefghijklmnopqrstuvwxyz
console.log(buf1.toString('ascii'));

// 输出: abcde
console.log(buf1.toString('ascii', 0, 5));


const buf2 = Buffer.from('tést');

// 输出: 74c3a97374
console.log(buf2.toString('hex'));

// 输出: té
console.log(buf2.toString('utf8', 0, 3));

// 输出: té
console.log(buf2.toString(undefined, 0, 3));
```

