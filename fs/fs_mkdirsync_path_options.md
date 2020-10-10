<!-- YAML
added: v0.1.21
changes:
  - version: v13.11.0
    pr-url: https://github.com/nodejs/node/pull/31530
    description: 在 `recursive` 模式中，会返回创建的第一个路径。
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/21875
    description: 第二个参数可以是 `options` 对象（具有 `recursive` 和 `mode` 属性）。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {string|integer} 在 Windows 上不支持。**默认值:** `0o777`。
* 返回: {string|undefined}

同步地创建目录。
返回 `undefined`，或创建的第一个目录的路径（如果 `recursive` 为 `true`）。
这是 [`fs.mkdir()`] 的同步版本。

也可参见 mkdir(2)。

