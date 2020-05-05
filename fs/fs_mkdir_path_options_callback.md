<!-- YAML
added: v0.1.8
changes:
  - version: v13.11.0
    pr-url: https://github.com/nodejs/node/pull/31530
    description: 在 `recursive` 模式中，回调会接收创建的第一个路径作为参数。
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/21875
    description: 第二个参数可以是 `options` 对象（具有 `recursive` 和 `mode` 属性）。
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {string|integer} 在 Windows 上不支持。**默认值:** `0o777`。
* `callback` {Function}
  * `err` {Error}

异步地创建目录。

回调会传入可能的异常、以及创建的第一个目录的路径（如果 `recursive` 为 `true`），`(err, [path])`。

可选的 `options` 参数可以是整数（指定 `mode`（权限和粘滞位））、或对象（具有 `mode` 属性和 `recursive` 属性（指示是否要创建父目录））。
当 `path` 是已存在的目录时，调用 `fs.mkdir()` 仅在 `recursive` 为 false 时才会导致错误。

```js
// 创建 `/目录1/目录2/目录3`，不管 `/目录1` 和 `/目录1/目录2` 是否存在。
fs.mkdir('/目录1/目录2/目录3', { recursive: true }, (err) => {
  if (err) throw err;
});
```

在 Windows 上，对根目录使用 `fs.mkdir()`（即使使用遍历）也会导致错误：

```js
fs.mkdir('/', { recursive: true }, (err) => {
  // => [Error: EPERM: operation not permitted, mkdir 'C:\']
});
```

也可参见 mkdir(2)。

