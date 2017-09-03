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
                 Thus for Node `< v6.3.0` use `fs` to access those constants, or
                 do something like `(fs.constants || fs).R_OK` to work with all
                 versions.
-->

* `path` {string|Buffer|URL}
* `mode` {integer} **Default:** `fs.constants.F_OK`
* `callback` {Function}

测试 `path` 指定的文件或目录的用户权限。
`mode` 是一个可选的整数，指定要执行的可访问性检查。
以下常量定义了 `mode` 的可能值。
可以创建由两个或更多个值的位或组成的掩码。

- `fs.constants.F_OK` - `path` 文件对调用进程可见。
这在确定文件是否存在时很有用，但不涉及 `rwx` 权限。
如果没指定 `mode`，则默认为该值。
- `fs.constants.R_OK` - `path` 文件可被调用进程读取。
- `fs.constants.W_OK` - `path` 文件可被调用进程写入。
- `fs.constants.X_OK` - `path` 文件可被调用进程执行。
对 Windows 系统没作用（相当于 `fs.constants.F_OK`）。

最后一个参数 `callback` 是一个回调函数，会带有一个可能的错误参数被调用。
如果可访问性检查有任何的失败，则错误参数会被传入。
下面的例子会检查 `/etc/passwd` 文件是否可以被当前进程读取和写入。

```js
fs.access('/etc/passwd', fs.constants.R_OK | fs.constants.W_OK, (err) => {
  console.log(err ? 'no access!' : 'can read/write');
});
```

不建议在调用 `fs.open()` 、 `fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.access()` 检查一个文件的可访问性。
如此处理会造成紊乱情况，因为其他进程可能在两个调用之间改变该文件的状态。
作为替代，用户代码应该直接打开/读取/写入文件，当文件无法访问时再处理错误。

例子：


**写入（不推荐）**

```js
fs.access('myfile', (err) => {
  if (!err) {
    console.error('myfile already exists');
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
      console.error('myfile already exists');
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
      console.error('myfile does not exist');
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
      console.error('myfile does not exist');
      return;
    }

    throw err;
  }

  readMyData(fd);
});
```

以上**不推荐**的例子检查可访问性之后再使用文件；
**推荐**的例子更好，因为它们直接使用文件并处理任何错误。

通常，仅在文件不会被直接使用时才检查一个文件的可访问性，例如当它的可访问性是来自另一个进程的信号。

