<!-- YAML
added: v0.11.15
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `mode` {integer} **Default:** `fs.constants.F_OK`
* 返回: `undefined`

同步地测试 `path` 指定的文件或目录的用户权限。 `mode` 是一个可选的整数，指定要执行的可访问性检查。 以下常量定义了 mode 的可能值。 可以创建由两个或更多个值的位或组成的掩码（例如 fs.constants.W_OK | fs.constants.R_OK）。

* `fs.constants.F_OK` - `path` 文件对调用进程可见。 这在确定文件是否存在时很有用，但不涉及 `rwx` 权限。 如果没指定 `mode` ，则默认为该值
* `fs.constants.R_OK` - `path` 文件可被调用进程读取。
* `fs.constants.W_OK` - `path` 文件可被调用进程写入。
* `fs.constants.X_OK` - `path` 文件可被调用进程执行。 对 `Windows` 系统没作用（相当于 `fs.constants.F_OK`）。

如果可访问性检查有任何的失败，则错误参数会是一个 `Error` 对象。 否则返回 `undefined`。

```js
try {
  fs.accessSync('etc/passwd', fs.constants.R_OK | fs.constants.W_OK);
  console.log('can read/write');
} catch (err) {
  console.error('no access!');
}
```
