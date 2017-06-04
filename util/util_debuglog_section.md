<!-- YAML
added: v0.11.3
-->

* `section` {string} 一个字符串，指定要为应用的哪些部分创建 `debuglog` 函数。
  `debuglog` 函数要为哪些应用创建。
* 返回: {Function} 日志函数

`util.debuglog()` 方法用于创建一个函数，基于 `NODE_DEBUG` 环境变量的存在与否有条件地写入调试信息到 `stderr`。
如果 `section` 名称在环境变量的值中，则返回的函数类似于 [`console.error()`]。
否则，返回的函数是一个空操作。

例子：

```js
const util = require('util');
const debuglog = util.debuglog('foo');

debuglog('hello from foo [%d]', 123);
```

如果程序在环境中运行时带上 `NODE_DEBUG=foo`，则输出类似如下： 

```txt
FOO 3245: hello from foo [123]
```

其中 `3245` 是进程 id。
如果运行时没带上环境变量集合，则不会打印任何东西。

`NODE_DEBUG` 环境变量中可指定多个由逗号分隔的 `section` 名称。
例如：`NODE_DEBUG=fs,net,tls`。

