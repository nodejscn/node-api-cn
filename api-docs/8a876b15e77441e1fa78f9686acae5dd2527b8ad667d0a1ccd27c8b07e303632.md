
<!-- type=misc -->

Node.js 的 `require()` 函数的语义被设计得足够通用化，可以支持许多合理的目录结构。
包管理器程序（如 `dpkg`、`rpm` 和 `npm`）可以不用修改就能够从 Node.js 模块构建本地包。

以下是一个推荐的目录结构：

假设想要在 `/usr/lib/node/<some-package>/<some-version>` 目录中保存一个特定版本的包的内容。

包可以依赖于其他包。
为了安装包 `foo`，可能需要安装一个指定版本的 `bar` 包。
`bar` 包也可能有依赖，且在某些情况下，依赖可能有冲突或形成循环。

因为 Node.js 会查找它所加载的模块的实际路径（也就是说会解析符号链接），然后在 `node_modules` 目录中寻找它们的依赖，[如下所述](#modules_loading_from_node_modules_folders)，这种情况使用以下体系结构很容易解决：

* `/usr/lib/node/foo/1.2.3/` - `foo` 包的内容，版本 1.2.3。
* `/usr/lib/node/bar/4.3.2/` - `foo` 依赖的 `bar` 包的内容。
* `/usr/lib/node/foo/1.2.3/node_modules/bar` - `/usr/lib/node/bar/4.3.2/` 的符号链接。
* `/usr/lib/node/bar/4.3.2/node_modules/*` - `bar` 所依赖的包的符号链接

因此，即便存在循环依赖或依赖冲突，每个模块还是可以获得它所依赖的包的一个可用版本。

当 `foo` 包中的代码调用 `require('bar')`，它会获得符号链接 `/usr/lib/node/foo/1.2.3/node_modules/bar` 指向的版本。
然后，当 `bar` 包中的代码调用 `require('queue')`，它会获得符号链接 `/usr/lib/node/bar/4.3.2/node_modules/quux` 指向的版本。

此外，为了进一步优化模块查找过程，不要将包直接放在 `/usr/lib/node` 目录中，而是将它们放在 `/usr/lib/node_modules/<name>/<version>` 目录中。
这样 Node.js 就不会在 `/usr/node_modules` 或 `/node_modules` 目录中查找缺失的依赖。

为了使模块在 Node.js 的 REPL 中可用，可能需要将 `/usr/lib/node_modules` 目录添加到 `$NODE_PATH` 环境变量中。
由于在 `node_modules` 目录中查找模块使用的是相对路径，而调用 `require()` 的文件是基于实际路径的，因此包本身可以放在任何地方。

