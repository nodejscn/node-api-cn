<!-- YAML
added: v0.8.6
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
-->

* `fd` {integer}
* `len` {integer} 默认 = `0`
* `callback` {Function}

异步的 ftruncate(2)。
完成回调只有一个可能的异常参数。

如果文件描述符指向的文件大于 `len` 个字节，则只有前面 `len` 个字节会保留在文件中。

例子，下面的程序会只保留文件前4个字节。

```js
console.log(fs.readFileSync('temp.txt', 'utf8'));
// 输出: Node.js

// 获取要截断的文件的文件描述符
const fd = fs.openSync('temp.txt', 'r+');

// 截断文件至前4个字节
fs.ftruncate(fd, 4, (err) => {
  assert.ifError(err);
  console.log(fs.readFileSync('temp.txt', 'utf8'));
});
// 输出: Node
```

如果前面的文件小于 `len` 个字节，则扩展文件，且扩展的部分用空字节（'\0'）填充。例子：

```js
console.log(fs.readFileSync('temp.txt', 'utf-8'));
// 输出: Node.js

// 获取要截断的文件的文件描述符
const fd = fs.openSync('temp.txt', 'r+');

// 截断文件至前10个字节，但实际大小是7个字节
fs.ftruncate(fd, 10, (err) => {
  assert.ifError(err);
  console.log(fs.readFileSync('temp.txt'));
});
// 输出: <Buffer 4e 6f 64 65 2e 6a 73 00 00 00>
// ('Node.js\0\0\0' in UTF8)
```

最后3个字节是空字节（'\0'），用于补充超出的截断。

