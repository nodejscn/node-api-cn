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

检查 `path` 指定的文件或目录的用户权限。
`mode` 指定要执行的可访问性检查。
`mode` 可选的值参见[文件可访问性的常量][File Access Constants]。
可以使用两个或更多个值进行位或操作来创建掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

`callback` 只有一个参数 `err`。
如果可访问性检查失败，则 `err` 会是一个 `Error`。
例子，检查 `package.json` 是否存在、可读或可写。

```js
const file = 'package.json';

// 检查文件是否存在。
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

// 检查文件是否存在且可写。
fs.access(file, fs.constants.F_OK | fs.constants.W_OK, (err) => {
  if (err) {
    console.error(
      `${file} ${err.code === 'ENOENT' ? '不存在' : '只可读'}`);
  } else {
    console.log(`${file} 存在且可写`);
  }
});
```

不建议在调用 `fs.open()`、`fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.access()` 检查文件的可访问性。
因为其他进程可能在两个调用的间隙改变文件的状态。
应该直接打开、读取或写入文件，当文件无法访问时再处理错误。

写入文件（不推荐的用法）：

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

写入文件（推荐的用法）：

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

读取文件（不推荐的用法）：

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

读取文件（推荐的用法）：

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

以上例子中，不推荐的用法会先检查可访问性再使用文件，而推荐的用法会直接使用文件并处理任何错误。

通常仅在不直接使用文件时才检查可访问性，例如文件的可访问性是另一个进程的信号。

