<!-- YAML
added: v6.3.0
-->

当解析和缓存模块时，命令模块加载器保持符号连接。

默认情况下，当 Node.js 从一个被符号连接到另一块磁盘位置的路径加载一个模块时，Node.js 会解引用该连接，并使用模块的真实磁盘的实际路径，作为定位其他依赖模块的标识符和根路径。
大多数情况下，默认行为是可接受的。
但是，当使用符号连接的同行依赖，如下例子所描述的，如果 `moduleA` 试图引入 `moduleB` 作为一个同行依赖，默认行为就会抛出异常：

```text
{appDir}
 ├── app
 │   ├── index.js
 │   └── node_modules
 │       ├── moduleA -> {appDir}/moduleA
 │       └── moduleB
 │           ├── index.js
 │           └── package.json
 └── moduleA
     ├── index.js
     └── package.json
```

`--preserve-symlinks` 命令行标志命令 Node.js 使用模块的符号路径而不是真实路径，是符号连接的同行依赖能被找到。

注意，使用 `--preserve-symlinks` 会有其他方面的影响。
比如，如果符号连接的原生模块在依赖树里来自超过一个位置，它们会加载失败。
（Node.js 会将它们视为两个独立的模块，且会试图多次加载模块，造成抛出异常。）
