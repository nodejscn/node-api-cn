<!-- YAML
added: v5.10.0
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
  - version: v6.2.1
    pr-url: https://github.com/nodejs/node/pull/6828
    description: The `callback` parameter is optional now.
-->

* `prefix` {string}
* `options` {string|Object}
  * `encoding` {string} 默认 = `'utf8'`
* `callback` {Function}

创建一个唯一的临时目录。

生成六位随机字符附加到一个要求的 `prefix` 后面，然后创建一个唯一的临时目录。

创建的目录路径会作为字符串传给回调的第二个参数。

可选的 `options` 参数可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。

例子：

```js
fs.mkdtemp('/tmp/foo-', (err, folder) => {
  if (err) throw err;
  console.log(folder);
  // 输出: /tmp/foo-itXde2
});
```

**注意**：`fs.mkdtemp()` 方法会直接附加六位随机选择的字符串到 `prefix` 字符串。
例如，指定一个目录 `/tmp`，如果目的是要在 `/tmp` 里创建一个临时目录，则 `prefix` **必须** 以一个指定平台的路径分隔符（`require('path').sep`）结尾。

```js
// 新建的临时目录的父目录
const tmpDir = '/tmp';

// 该方法是 *错误的*：
fs.mkdtemp(tmpDir, (err, folder) => {
  if (err) throw err;
  console.log(folder);
  // 会输出类似于 `/tmpabc123`。
  // 注意，一个新的临时目录会被创建在文件系统的根目录，而不是在 /tmp 目录里。
});

// 该方法是 *正确的*：
const { sep } = require('path');
fs.mkdtemp(`${tmpDir}${sep}`, (err, folder) => {
  if (err) throw err;
  console.log(folder);
  // 会输出类似于 `/tmp/abc123`。
  // 一个新的临时目录会被创建在 /tmp 目录里。
});
```

