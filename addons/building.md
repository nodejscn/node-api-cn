
当源代码已被编写，它必须被编译成二进制 `addon.node` 文件。
要做到这点，需在项目的顶层创建一个名为 `binding.gyp` 的文件，它使用一个类似 JSON 的格式来描述模块的构建配置。
该文件会被 [node-gyp]（一个用于编译 Node.js 插件的工具）使用。


```json
{
  "targets": [
    {
      "target_name": "addon",
      "sources": [ "hello.cc" ]
    }
  ]
}
```

注意：Node.js 会捆绑与发布一个版本的 `node-gyp` 工具作为 `npm` 的一部分。
该版本不可以直接被开发者使用，仅为了支持使用 `npm install` 命令编译与安装插件的能力。
需要直接使用 `node-gyp` 的开发者可以使用 `npm install -g node-gyp` 命令进行安装。
查看 `node-gyp` [安装说明]了解更多信息，包括平台特定的要求。

但 `binding.gyp` 文件已被创建，使用 `node-gyp configure` 为当前平台生成相应的项目构建文件。
这会在 `build/` 目录下生成一个 `Makefile` 文件（在 Unix 平台上）或 `vcxproj` 文件（在 Windows 上）。

下一步，调用 `node-gyp build` 命令生成编译后的 `addon.node` 的文件。
它会被放进 `build/Release/` 目录。

当使用 `npm install` 安装一个 Node.js 插件时，npm 会使用自身捆绑的 `node-gyp` 版本来执行同样的一套动作，为用户要求的平台生成一个插件编译后的版本。

当构建完成时，二进制插件就可以在 Node.js 中被使用，通过 [`require()`] 构建后的 `addon.node` 模块：

```js
// hello.js
const addon = require('./build/Release/addon');

console.log(addon.hello());
// 打印: 'world'
```

请查看 <https://github.com/arturadib/node-qt> 了解生产环境中的例子。

因为编译后的二进制插件的确切路径取决于它如何被编译（比如有时它可能在 `./build/Debug/` 中），所以插件可以使用 [bindings] 包加载编译后的模块。

注意，虽然 `bindings` 包在如何定位插件模块的实现上更复杂，但它本质上使用了一个 `try-catch` 模式，类似如下：

```js
try {
  return require('./build/Release/addon.node');
} catch (err) {
  return require('./build/Debug/addon.node');
}
```

