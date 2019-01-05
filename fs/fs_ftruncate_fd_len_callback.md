<!-- YAML
added: v0.8.6
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
-->

* `fd` {integer}
* `len` {integer} 默认为 `0`。
* `callback` {Function}
  * `err` {Error}

异步的 ftruncate(2)。
除了可能的异常，完成回调没有其他参数。

如果文件描述符指向的文件大于 `len` 个字节，则只有前面 `len` 个字节会保留在文件中。

例子，只保留文件的前 4 个字节。

```js
console.log(fs.readFileSync('文件.txt', 'utf8'));
// 打印: Node.js

// 获取要截断的文件的文件描述符。
const fd = fs.openSync('文件.txt', 'r+');

// 截断文件至前 4 个字节。
fs.ftruncate(fd, 4, (err) => {
  assert.ifError(err);
  console.log(fs.readFileSync('文件.txt', 'utf8'));
});
// 打印: Node
```

如果文件小于 `len` 个字节，则扩大文件，且扩大的部分用空字节（`'\0'`）填充：

```js
console.log(fs.readFileSync('文件.txt', 'utf8'));
// 打印: Node.js

// 获取要截断的文件的文件描述符。
const fd = fs.openSync('文件.txt', 'r+');

// 截断文件至前 10 个字节，但实际大小只有 7 个字节。
fs.ftruncate(fd, 10, (err) => {
  assert.ifError(err);
  console.log(fs.readFileSync('文件.txt'));
});
// 打印: <Buffer 4e 6f 64 65 2e 6a 73 00 00 00>
// (UTF8 的值为 'Node.js\0\0\0')
```

最后3个字节是空字节（`'\0'`），用于补充超出的截断。

