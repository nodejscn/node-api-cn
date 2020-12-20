<!-- YAML
added: v3.0.0
changes:
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3212
    description: The `lts` property is now supported.
-->

* {Object}

`process.release` 属性返回与当前发布相关的元数据 `Object`，包括源代码和源代码头文件 tarball 的 URL。

`process.release` 包括如下属性：

* `name` {string} 此值始终为 `'node'`。
* `sourceUrl` {string} 指向一个_`.tar.gz`_文件的绝对 URL，包括了当前发布的源代码。
* `headersUrl`{string} 指向一个_`.tar.gz`_文件的绝对 URL，包括了当前发布的源代码的头文件信息。
  这个文件要比全部源代码文件明显小很多，可以用于编译 Node.js 原生插件。
* `libUrl` {string} 指向一个_`node.lib`_文件的绝对 URL，匹配当前发布的结构和版本信息。此文件用于编译 Node.js 本地插件。这个属性只在 Windows 版本中存在，在其他平台中无效。
* `lts` {string} 标识当前发布的 [LTS][] 标签的字符串。
  只有 LTS 版本存在这个属性，其他所有版本类型（包括当前版本）这个属性都是 `undefined`。
  有效值包括 LTS 发行代号（包括不再受支持的代号）。 
  这些代号的非穷举示例包括：
  * `'Dubnium'` 用于 10.13.0 开始的 10.x LTS 版本。
  * `'Erbium'` 用于 12.13.0 开始的 12.x LTS 版本。
  有关其他的 LTS 发行代号，参见 [Node.js 更新日志的存档](https://github.com/nodejs/node/blob/master/doc/changelogs/CHANGELOG_ARCHIVE.md)。

<!-- eslint-skip -->
```js
{
  name: 'node',
  lts: 'Erbium',
  sourceUrl: 'https://nodejs.org/download/release/v12.18.1/node-v12.18.1.tar.gz',
  headersUrl: 'https://nodejs.org/download/release/v12.18.1/node-v12.18.1-headers.tar.gz',
  libUrl: 'https://nodejs.org/download/release/v12.18.1/win-x64/node.lib'
}
```

从源码树的非发布版本中构建的定制版本，可能只有 `name` 属性有效。其他的属性不一定会存在。

