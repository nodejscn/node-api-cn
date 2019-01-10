<!-- YAML
added: v0.1.90
-->

* `encoding` {string} 使用的字符编码。默认为 `'utf8'`。
* `start` {integer} 开始解码的字节偏移量。默认为 `0`。
* `end` {integer} 结束解码的字节偏移量（不包含）。默认为 [`buf.length`]。
* 返回: {string}

根据 `encoding` 指定的字符编码将 `buf` 解码成字符串。

字符串的最大长度（以 UTF-16 为单位）可查看 [`buffer.constants.MAX_STRING_LENGTH`]。

```js
const buf1 = Buffer.allocUnsafe(26);

for (let i = 0; i < 26; i++) {
  // 97 是 'a' 的十进制 ASCII 值。
  buf1[i] = i + 97;
}

console.log(buf1.toString('ascii'));
// 输出: abcdefghijklmnopqrstuvwxyz
console.log(buf1.toString('ascii', 0, 5));
// 输出: abcde

const buf2 = Buffer.from('tést');

console.log(buf2.toString('hex'));
// 输出: 74c3a97374
console.log(buf2.toString('utf8', 0, 3));
// 输出: té
console.log(buf2.toString(undefined, 0, 3));
// 输出: té
```

