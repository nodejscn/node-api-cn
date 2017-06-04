
<!-- type=misc -->

如果 `NODE_PATH` 环境变量被设为一个以冒号分割的绝对路径列表，则当在其他地方找不到模块时 Node.js 会搜索这些路径。

注意：在 Windows 系统中，`NODE_PATH` 是以分号间隔的。

在当前的[模块解析]算法运行之前，`NODE_PATH` 最初是创建来支持从不同路径加载模块的。

虽然 `NODE_PATH` 仍然被支持，但现在不太需要，因为 Node.js 生态系统已制定了一套存放依赖模块的约定。
有时当人们没意识到 `NODE_PATH` 必须被设置时，依赖 `NODE_PATH` 的部署会出现意料之外的行为。
有时一个模块的依赖会改变，导致在搜索 `NODE_PATH` 时加载了不同的版本（甚至不同的模块）。

此外，Node.js 还会搜索以下位置：

* 1: `$HOME/.node_modules`
* 2: `$HOME/.node_libraries`
* 3: `$PREFIX/lib/node`

其中 `$HOME` 是用户的主目录，`$PREFIX` 是 Node.js 里配置的 `node_prefix`。

这些主要是历史原因。

注意：强烈建议将所有的依赖放在本地的 `node_modules` 目录。
这样将会更快地加载，且更可靠。

