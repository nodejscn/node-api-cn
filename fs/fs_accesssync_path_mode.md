<!-- YAML
added: v0.11.15
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `mode` {integer} **默认值:** `fs.constants.F_OK`。

同步地测试用户对 `path` 指定的文件或目录的权限。
`mode` 参数是一个可选的整数，指定要执行的可访问性检查。
查看[文件可访问性的常量][File Access Constants]了解 `mode` 的可选值。 
可以创建由两个或更多个值按位或组成的掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

如果可访问性检查失败，则抛出 `Error`。
否则，该方法将返回 `undefined`。

```js
try {
  fs.accessSync('etc/passwd', fs.constants.R_OK | fs.constants.W_OK);
  console.log('可以读写');
} catch (err) {
  console.error('无权访问');
}
```

