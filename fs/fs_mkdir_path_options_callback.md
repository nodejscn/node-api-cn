<!-- YAML
added: v0.1.8
changes:
  - version: v13.11.0
    pr-url: https://github.com/nodejs/node/pull/31530
    description: In `recursive` mode, the callback now receives the first
                 created path as an argument.
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/21875
    description: The second argument can now be an `options` object with
                 `recursive` and `mode` properties.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {string|integer} Windows 上不支持。**默认值:** `0o777`。
* `callback` {Function}
  * `err` {Error}

异步地创建目录。

回调会带上可能的异常，如果 `recursive` 为 `true`，则会带上创建的第一个文件夹的路径，`(err, [path])`。

可选的 `options` 参数可以是指定模式（权限和粘滞位）的整数，也可以是具有 `mode` 属性和 `recursive` 属性（指示是否应创建父文件夹）的对象。

```js
// 创建 /tmp/a/apple 目录，无论是否存在 /tmp 和 /tmp/a 目录。
fs.mkdir('/tmp/a/apple', { recursive: true }, (err) => {
  if (err) throw err;
});
```

在 Windows 上，在根目录上使用 `fs.mkdir()` （即使使用递归参数）也会导致错误：

```js
fs.mkdir('/', { recursive: true }, (err) => {
  // => [Error: EPERM: operation not permitted, mkdir 'C:\']
});
```

也可参阅 mkdir(2)。

