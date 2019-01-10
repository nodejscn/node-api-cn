<!-- YAML
added: v0.7.7
-->

* {Object}

`process.execArgv` 属性返回当Node.js进程被启动时，Node.js特定的命令行选项。
这些选项在[`process.argv`][]属性返回的数组中不会出现，并且这些选项中不会包括Node.js的可执行脚本名称或者任何在脚本名称后面出现的选项。
这些选项在创建子进程时是有用的，因为他们包含了与父进程一样的执行环境信息。

例如:

```console
$ node --harmony script.js --version
```

`process.execArgv`的结果:

<!-- eslint-disable semi -->
```js
['--harmony']
```

`process.argv`的结果:

<!-- eslint-disable semi -->
```js
['/usr/local/bin/node', 'script.js', '--version']
```

