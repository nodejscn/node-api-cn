<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `mode` {integer} **默认值:** `fs.constants.F_OK`。
* 返回: {Promise}

测试用户对 `path` 指定的文件或目录的权限。 
`mode` 参数是一个可选的整数，指定要执行的可访问性检查。
`mode` 可选的值参阅[文件可访问性的常量][File Access Constants]。 
可以创建由两个或更多个值按位或组成的掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

如果可访问性检查成功，则 `Promise` 会被解决且不带值。 
如果任何可访问性检查失败，则 `Promise` 会被拒绝并带上 `Error` 对象。 
以下示例会检查当前进程是否可以读取和写入 `/etc/passwd` 文件。

```js
const fs = require('fs');
const fsPromises = fs.promises;

fsPromises.access('/etc/passwd', fs.constants.R_OK | fs.constants.W_OK)
  .then(() => console.log('可以访问'))
  .catch(() => console.error('不可访问'));
```

不建议在调用 `fsPromises.open()` 之前使用 `fsPromises.access()` 检查文件的可访问性。 
这样做会引入竞态条件，因为其他进程可能会在两个调用之间更改文件的状态。 
相反，应该直接打开、读取或写入文件，如果文件无法访问则处理引发的错误。

