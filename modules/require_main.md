<!-- YAML
added: v0.1.17
-->

* {module}

`Module` 对象，表示当 Node.js 进程启动时加载的入口脚本。 
参见[访问主模块]。

在 `entry.js` 脚本中：

```js
console.log(require.main);
```

```sh
node entry.js
```

<!-- eslint-skip -->
```js
Module {
  id: '.',
  exports: {},
  parent: null,
  filename: '/absolute/path/to/entry.js',
  loaded: false,
  children: [],
  paths:
   [ '/absolute/path/to/node_modules',
     '/absolute/path/node_modules',
     '/absolute/node_modules',
     '/node_modules' ] }
```

