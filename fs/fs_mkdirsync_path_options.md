<!-- YAML
added: v0.1.21
changes:
  - version: v13.11.0
    pr-url: https://github.com/nodejs/node/pull/31530
    description: In `recursive` mode, the first created path is returned now.
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/21875
    description: The second argument can now be an `options` object with
                 `recursive` and `mode` properties.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {string|integer} Windows 上不支持。**默认值:** `0o777`。
* 返回: {string|undefined}

同步地创建目录。
返回 `undefined`，或者如果 `recursive` 为 `true`，则返回创建的第一个文件夹的路径。
[`fs.mkdir()`] 的同步版本。

也可参阅 mkdir(2)。

