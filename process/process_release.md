<!-- YAML
added: v3.0.0
changes:
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3212
    description: The `lts` property is now supported.
-->

`process.release` 属性返回与当前发布相关的元数据对象，包括源代码和源代码头文件 tarball的URLs。


`process.release`包括如下属性：

* `name` {string} 对于Node.js， 此值始终为`'node'`。对于传统io.js 发布包， 此值为`'io.js'`。

* `sourceUrl` {string} 指向一个_`.tar.gz`_文件的绝对URL，包括了当前发布的源代码。

* `headersUrl`{string} 指向一个_`.tar.gz`_文件的绝对URL，包括了当前发布的源代码的头文件信息。
  这个文件要比全部源代码文件明显小很多，可以用于编译Node.js原生插件。

* `libUrl` {string} 指向一个_`node.lib`_文件的绝对URL，匹配当前发布的结构和版本信息。此文件用于编译Node.js本地插件。
  _这个属性只在Windows版本中存在，在其他平台中无效。

* `lts` {string} 标识当前发布的[LTS][]标签的字符串。 如果Node.js发布不是一个LTS发布，此值为`undefined`。

例如：

<!-- eslint-skip -->
```js
{
  name: 'node',
  lts: 'Argon',
  sourceUrl: 'https://nodejs.org/download/release/v4.4.5/node-v4.4.5.tar.gz',
  headersUrl: 'https://nodejs.org/download/release/v4.4.5/node-v4.4.5-headers.tar.gz',
  libUrl: 'https://nodejs.org/download/release/v4.4.5/win-x64/node.lib'
}
```

从源码树的非发布版本中构建的定制版本，可能只有`name`属性有效。其他的属性不一定会存在。

