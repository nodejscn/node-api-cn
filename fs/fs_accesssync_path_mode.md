<!-- YAML
added: v0.11.15
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `mode` {integer} 默认为 `fs.constants.F_OK`。

同步地检测 `path` 指定的文件或目录的用户权限。
`mode` 参数是一个可选的整数，指定要执行的可访问性检查。 
[文件可访问性的常量][File Access Constants]定义了 `mode` 可选的值。
可以创建由两个或更多个值的位或组成的掩码（例如 fs.constants.W_OK | fs.constants.R_OK）。

如果可访问性检查失败，则抛出一个 `Error` 对象，否则返回 `undefined`。

```js
try {
  fs.accessSync('etc/passwd', fs.constants.R_OK | fs.constants.W_OK);
  console.log('可读可写');
} catch (err) {
  console.error('不可访问！');
}
```

