<!-- YAML
added: v5.10.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v6.2.1
    pr-url: https://github.com/nodejs/node/pull/6828
    description: The `callback` parameter is optional now.
-->

* `prefix` {string}
* `options` {string|Object}
  * `encoding` {string} 默认为 `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `folder` {string}

创建临时目录。

生成六位随机字符附加到要求的 `prefix` 后面，然后创建一个唯一的临时目录。

创建的目录路径会作为字符串传给回调的第二个参数。

`options` 参数可以是一个字符串，指定字符编码。
也可以是一个对象，其中 `encoding` 属性指定字符编码。

例子：

```js
fs.mkdtemp(path.join(os.tmpdir(), '目录-'), (err, folder) => {
  if (err) throw err;
  console.log(folder);
  // 打印: /tmp/目录-itXde2 或 C:\Users\...\AppData\Local\Temp\目录-itXde2
});
```

`fs.mkdtemp()` 会直接附加六位随机选择的字符串到 `prefix` 字符串。
例如，指定目录 `/tmp`，如果要在 `/tmp` 里面创建临时目录，则 `prefix` 必须在结尾加上指定平台的路径分隔符（`require('path').sep`）。

```js
// 新建的临时目录的父目录。
const tmpDir = os.tmpdir();

// 该使用方法是错误的：
fs.mkdtemp(tmpDir, (err, folder) => {
  if (err) throw err;
  console.log(folder);
  // 会打印 `/tmpabc123`。
  // 新的临时目录会被创建到文件系统的根目录，而不是在 /tmp 目录里。
});

// 该使用方法才是正确的：
const { sep } = require('path');
fs.mkdtemp(`${tmpDir}${sep}`, (err, folder) => {
  if (err) throw err;
  console.log(folder);
  // 会打印于 `/tmp/abc123`。
  // 新的临时目录会被创建在 /tmp 目录里。
});
```

