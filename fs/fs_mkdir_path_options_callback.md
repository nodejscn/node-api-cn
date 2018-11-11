<!-- YAML
added: v0.1.8
changes:
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
  * `recursive` {boolean} 默认为 `false`。
  * `mode` {integer} 不支持 Windows 平台。默认为 `0o777`。
* `callback` {Function}
  * `err` {Error}

异步地创建目录。
完成回调只有一个可能的异常参数。

`options` 参数可以是一个整数，用于指定文件的模式（权限与粘滞位）。
也可以是一个对象，其中 `recursive` 属性指定是否创建父目录。

```js
// 创建 /tmp/a/apple 目录，不管 `/tmp` 和 /tmp/a 目录是否存在。
fs.mkdir('/tmp/a/apple', { recursive: true }, (err) => {
  if (err) throw err;
});
```

详见 mkdir(2)。

