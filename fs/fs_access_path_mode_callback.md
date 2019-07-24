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
* `mode` {integer} **默认值:** `fs.constants.F_OK`。
* `callback` {Function}
  * `err` {Error}

测试用户对 `path` 指定的文件或目录的权限。
`mode` 参数是一个可选的整数，指定要执行的可访问性检查。
`mode` 可选的值参阅[文件可访问性的常量][File Access Constants]。
可以创建由两个或更多个值按位或组成的掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

最后一个参数 `callback` 是一个回调函数，调用时将传入可能的错误参数。
如果可访问性检查失败，则错误参数将是 `Error` 对象。
以下示例检查 `package.json` 是否存在，以及它是否可读或可写。

```js
const file = 'package.json';

// 检查当前目录中是否存在该文件。
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

// 检查当前目录中是否存在该文件，以及该文件是否可写。
fs.access(file, fs.constants.F_OK | fs.constants.W_OK, (err) => {
  if (err) {
    console.error(
      `${file} ${err.code === 'ENOENT' ? '不存在' : '只可读'}`);
  } else {
    console.log(`${file} 存在，且它是可写的`);
  }
});
```

不建议在调用 `fs.open()`、`fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.access()` 检查文件的可访问性。
这样做会引入竞态条件，因为其他进程可能会在两个调用之间更改文件的状态。
相反，应该直接打开、读取或写入文件，如果文件无法访问则处理引发的错误。

**写入（不推荐）**

```js
fs.access('myfile', (err) => {
  if (!err) {
    console.error('myfile 已存在');
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
      console.error('myfile 已存在');
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
      console.error('myfile 不存在');
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
      console.error('myfile 不存在');
      return;
    }

    throw err;
  }

  readMyData(fd);
});
```

上面的“不推荐”示例会先检查可访问性，然后再使用文件。
“推荐”示例则更好，因为它们直接使用文件并处理错误（如果有错误的话）。

通常，仅在不直接使用文件时才检查文件的可访问性，例如当其可访问性是来自其他进程的信号时。

在 Windows 上，目录上的访问控制策略（ACL）可能会限制对文件或目录的访问。
但是，`fs.access()` 函数不检查 ACL，因此即使 ACL 限制用户读取或写入路径，也可能报告路径是可访问的。

