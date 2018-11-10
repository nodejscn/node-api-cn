<!-- YAML
added: v8.5.0
-->

* `src` {string|Buffer|URL} 要拷贝的来源文件名。
* `dest` {string|Buffer|URL} 拷贝操作的目标文件名。
* `flags` {number} 拷贝操作的修饰符。默认为 `0`。
* `callback` {Function}

异步地将 `src` 拷贝到 `dest`。
默认情况下，如果 `dest` 已存在则覆盖。
回调函数只有一个可能的异常参数。
Node.js 不能保证拷贝操作的原子性。
如果目标文件打开后出现错误，Node.js 会尝试删除它。

`flags` 是一个可选的整数，用于指定拷贝操作的行为。
可以使用两个或更多个值进行位或操作来创建掩码（比如 `fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`）。

* `fs.constants.COPYFILE_EXCL` - 如果 `dest` 已存在，则拷贝操作会失败。
* `fs.constants.COPYFILE_FICLONE` - 拷贝操作会试图创建一个写时拷贝（copy-on-write）链接。
  如果平台不支持写时拷贝，则使用备选的拷贝机制。
* `fs.constants.COPYFILE_FICLONE_FORCE` - 拷贝操作会试图创建一个写时拷贝链接。
  如果平台不支持写时拷贝，则拷贝操作会失败。

```js
const fs = require('fs');

// 默认情况下，目标文件.txt 会被创建或覆盖。
fs.copyFile('来源文件.txt', '目标文件.txt', (err) => {
  if (err) throw err;
  console.log('来源文件.txt 已拷贝到 目标文件.txt');
});
```

如果第三个参数是数字，则指定 `flags`，例如:  

```js
const fs = require('fs');
const { COPYFILE_EXCL } = fs.constants;

// 因为使用了 COPYFILE_EXCL，如果 目标文件.txt 已存在，则操作失败。
fs.copyFile('来源文件.txt', '目标文件.txt', COPYFILE_EXCL, callback);
```

