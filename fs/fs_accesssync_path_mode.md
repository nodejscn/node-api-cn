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

同步地检查 `path` 指定的文件或目录的用户权限。
`mode` 指定要执行的可访问性检查。 
`mode` 可选的值参见[文件可访问性的常量][File Access Constants]。
可以使用两个或更多个值进行位或操作来创建掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

如果可访问性检查失败，则抛出异常，否则返回 `undefined`。

```js
try {
  fs.accessSync('etc/passwd', fs.constants.R_OK | fs.constants.W_OK);
  console.log('可读可写');
} catch (err) {
  console.error('不可访问');
}
```

