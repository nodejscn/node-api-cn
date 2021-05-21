
<!-- type=misc -->

当一个文件被从 Node.js 直接地运行时，则 `require.main` 被设置为它的 `module`。
这意味着可以通过测试 `require.main === module` 来判断一个文件是否被直接地运行。

对于一个文件 `foo.js`，如果通过 `node foo.js` 运行则这会是 `true`，但是如果通过 `require('./foo')` 运行则为 `false`。

因为 `module` 提供了一个 `filename` 属性（通常等效于 `__filename`），所以当前应用程序的入口点可以被通过检查 `require.main.filename` 获取。

