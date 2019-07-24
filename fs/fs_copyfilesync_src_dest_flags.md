<!-- YAML
added: v8.5.0
-->

* `src` {string|Buffer|URL} 要拷贝的源文件名。
* `dest` {string|Buffer|URL} 拷贝操作的目标文件名。
* `flags` {number} 用于拷贝操作的修饰符。**默认值:** `0`。

同步地将 `src` 拷贝到 `dest`。
默认情况下，如果 `dest` 已经存在，则覆盖它。
返回 `undefined`。
Node.js 不保证拷贝操作的原子性。
如果在打开目标文件用于写入后发生错误，则 Node.js 将尝试删除目标文件。

`flags` 是一个可选的整数，指定拷贝操作的行为。
可以创建由两个或更多个值按位或组成的掩码（比如 `fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`）。

* `fs.constants.COPYFILE_EXCL` - 如果 `dest` 已存在，则拷贝操作将失败。
* `fs.constants.COPYFILE_FICLONE` - 拷贝操作将尝试创建写时拷贝（copy-on-write）链接。如果平台不支持写时拷贝，则使用后备的拷贝机制。
* `fs.constants.COPYFILE_FICLONE_FORCE` - 拷贝操作将尝试创建写时拷贝链接。如果平台不支持写时拷贝，则拷贝操作将失败。

```js
const fs = require('fs');

// 默认情况下将创建或覆盖目标文件。
fs.copyFileSync('源文件.txt', '目标文件.txt');
console.log('源文件已拷贝到目标文件');
```

如果第三个参数是数字，则它指定 `flags`:  

```js
const fs = require('fs');
const { COPYFILE_EXCL } = fs.constants;

// 通过使用 COPYFILE_EXCL，如果目标文件存在，则操作将失败。
fs.copyFileSync('源文件.txt', '目标文件.txt', COPYFILE_EXCL);
```

