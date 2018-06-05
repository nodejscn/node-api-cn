<!-- YAML
added: v0.11.15
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/6534
    description: The constants like `fs.R_OK`, etc which were present directly
                 on `fs` were moved into `fs.constants` as a soft deprecation.
                 Thus for Node.js `< v6.3.0` use `fs`
                 to access those constants, or
                 do something like `(fs.constants || fs).R_OK` to work with all
                 versions.
-->

* `path` {string|Buffer|URL}
* `mode` {integer} 默认为 `fs.constants.F_OK`。
* `callback` {Function}
  * `err` {Error}

测试 `path` 指定的文件或目录的用户权限。
`mode` 参数是一个可选的整数，指定要执行的可访问性检查。
[文件访问常量]定义了 `mode` 可选的值。
可以创建由两个或更多个值的位或组成的掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

最后一个参数 `callback` 是一个回调函数，会传入一个可能的错误参数。
如果可访问性检查失败，则错误参数会是一个 `Error` 对象。
下面的例子会检查 `package.json` 文件是否存在，且是否可读或可写。

```js
const file = 'package.json';

// 检查文件是否存在于当前目录。
fs.access(file, fs.constants.F_OK, (err) => {
  console.log(`${file} ${err ? '不存在' : '存在'}`);
});

// 检查文件是否可读。
fs.access(file, fs.constants.R_OK, (err) => {
  console.log(`${file} ${err ? '不可读' : '可读'}`);
});

// 检查文件是否可写。
fs.access(file, fs.constants.W_OK, (err) => {
  console.log(`${file} ${err ? '不可写' : '可写'}`);
});

// 检查文件是否存在于当前目录，且是否可写。
fs.access(file, fs.constants.F_OK | fs.constants.W_OK, (err) => {
  if (err) {
    console.error(
      `${file} ${err.code === 'ENOENT' ? '不存在' : '只可读'}`);
  } else {
    console.log(`${file} 存在，且可写`);
  }
});
```

不建议在调用 `fs.open()` 、 `fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.access()` 检查一个文件的可访问性。
如此处理会造成紊乱情况，因为其他进程可能在两个调用之间改变该文件的状态。
所以，用户代码应该直接打开/读取/写入文件，当文件无法访问时再处理错误。

**写入（不推荐）**

```js
fs.access('myfile', (err) => {
  if (!err) {
    console.error('文件已存在');
    return;
  }

  fs.open('myfile', 'wx', (err, fd) => {
    if (err) throw err;
    writeMyData(fd);
  });
});
```

**写入（推荐）**

```js
fs.open('myfile', 'wx', (err, fd) => {
  if (err) {
    if (err.code === 'EEXIST') {
      console.error('文件已存在');
      return;
    }

    throw err;
  }

  writeMyData(fd);
});
```

**读取（不推荐）**

```js
fs.access('myfile', (err) => {
  if (err) {
    if (err.code === 'ENOENT') {
      console.error('文件不存在');
      return;
    }

    throw err;
  }

  fs.open('myfile', 'r', (err, fd) => {
    if (err) throw err;
    readMyData(fd);
  });
});
```

**读取（推荐）**

```js
fs.open('myfile', 'r', (err, fd) => {
  if (err) {
    if (err.code === 'ENOENT') {
      console.error('文件不存在');
      return;
    }

    throw err;
  }

  readMyData(fd);
});
```

以上**不推荐**的例子会检查可访问性之后再使用文件；
但**推荐**的例子更好，因为它们直接使用文件并处理任何错误。

通常，仅在文件不会被直接使用时才检查一个文件的可访问性，例如当它的可访问性是来自另一个进程的信号。

