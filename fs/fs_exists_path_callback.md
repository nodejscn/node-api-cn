<!-- YAML
added: v0.0.2
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
deprecated: v1.0.0
-->

> 稳定性: 0 - 废弃: 改为使用 [`fs.stat()`] 或 [`fs.access()`]。

* `path` {string|Buffer|URL}
* `callback` {Function}
  * `exists` {boolean}

通过检查文件系统来测试给定的路径是否存在。
然后调用 `callback` 并带上参数 `true` 或 `false`：

```js
fs.exists('/etc/passwd', (exists) => {
  console.log(exists ? '存在' : '不存在');
});
```

此回调的参数与其他 Node.js 回调不一致。
通常，Node.js 回调的第一个参数是 `err` 参数，后面可选地跟随其他参数。 
`fs.exists()` 的回调只有一个布尔值参数。
这是推荐 `fs.access()` 代替 `fs.exists()` 的原因之一。

不建议在调用 `fs.open()`、`fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.exists()` 检查文件是否存在。
这样做会引入竞态条件，因为其他进程可能会在两次调用之间更改文件的状态。
相反，应该直接打开、读取或写入文件，如果文件不存在则处理引发的错误。


**写入（不推荐）**

```js
fs.exists('myfile', (exists) => {
  if (exists) {
    console.error('myfile 已存在');
  } else {
    fs.open('myfile', 'wx', (err, fd) => {
      if (err) throw err;
      writeMyData(fd);
    });
  }
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
fs.exists('myfile', (exists) => {
  if (exists) {
    fs.open('myfile', 'r', (err, fd) => {
      if (err) throw err;
      readMyData(fd);
    });
  } else {
    console.error('myfile 不存在');
  }
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

上面的“不推荐”示例会先检查文件是否存在然后再使用该文件。
“推荐”示例则更好，因为它们直接使用文件并处理错误（如果有错误的话）。

通常，仅在文件不直接使用时才检查文件是否存在，例如当其存在性是来自另一个进程的信号时。


