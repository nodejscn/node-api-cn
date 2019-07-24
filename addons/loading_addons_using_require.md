
编译后的二进制插件的文件扩展名是 `.node`（而不是 `.dll` 或 `.so`）。
[`require()`] 函数用于查找具有 `.node` 文件扩展名的文件，并初始化为动态链接库。

当调用 [`require()`] 时，`.node` 拓展名通常可被省略，Node.js 仍会找到并初始化该插件。
注意，Node.js 会优先尝试查找并加载同名的模块或 JavaScript 文件。
例如，如果与二进制的 `addon.node` 同一目录下有一个 `addon.js` 文件，则 [`require('addon')`] 会优先加载 `addon.js` 文件。

