
<!--type=misc-->

可以把程序和库放到一个单独的目录，然后提供一个单一的入口来指向它。
把目录递给 `require()` 作为一个参数，有三种方式。

第一种方式是在根目录下创建一个 `package.json` 文件，并指定一个 `main` 模块。
例子，`package.json` 文件类似：

```json
{ "name" : "some-library",
  "main" : "./lib/some-library.js" }
```

如果这是在 `./some-library` 目录中，则 `require('./some-library')` 会试图加载 `./some-library/lib/some-library.js`。

这就是 Node.js 处理 `package.json` 文件的方式。

注意：如果 `package.json` 中 `"main"` 入口指定的文件不存在，则无法解析，Node.js 会将模块视为不存在，并抛出默认错误：

```txt
Error: Cannot find module 'some-library'
```

如果目录里没有 `package.json` 文件，则 Node.js 就会试图加载目录下的 `index.js` 或 `index.node` 文件。
例如，如果上面的例子中没有 `package.json` 文件，则 `require('./some-library')` 会试图加载：

* `./some-library/index.js`
* `./some-library/index.node`

