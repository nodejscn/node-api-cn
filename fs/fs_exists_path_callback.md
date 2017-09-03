<!-- YAML
added: v0.0.2
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
deprecated: v1.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`fs.stat()`] 或 [`fs.access()`] 代替。

* `path` {string|Buffer|URL}
* `callback` {Function}

通过检查文件系统来测试给定的路径是否存在。然后使用 true 或 false 为参数调用 `callback`。例子：

```js
fs.exists('/etc/passwd', (exists) => {
  console.log(exists ? 'it\'s there' : 'no passwd!');
});
```

**注意此回调的参数和其他 Node.js 回调的参数不一致。** 通常，Node.js 回调的第一个参数是 `err`, 接下来是一些其他可选参数。 `fs.exists()` 只有一个布尔类型的参数。这也是为什么推荐使用 `fs.access()` 代替 `fs.exists()`。

不推荐在调用 `fs.open`，`fs.readFile()`，`fs.writeFile()` 之前使用 `fs.exists()` 检测文件是否存在。这样做会引起竞争条件，因为在两次调用之间，其他进程可能修改文件。作为替代，用户应该直接开/读取/写入文件，当文件不存在时再处理错误。

例子：

**write (不推荐)**

```js
fs.exists('myfile', (exists) => {
  if (exists) {
    console.error('myfile already exists');
  } else {
    fs.open('myfile', 'wx', (err, fd) => {
      if (err) throw err;
      writeMyData(fd);
    });
  }
});
```

**write (不推荐)**

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

**read (不推荐)**

```js
fs.exists('myfile', (exists) => {
  if (exists) {
    fs.open('myfile', 'r', (err, fd) => {
      readMyData(fd);
    });
  } else {
    console.error('myfile does not exist');
  }
});
```

**read (推荐)**

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

上面这些 **不推荐** 的例子先检测文件是否存在再使用文件；**推荐** 的例子更好因为它直接使用文件并处理任何错误。

通常，仅在文件不会被直接使用时才检查一个文件的可访问性，例如当它的可访问性是来自另一个进程的信号。

