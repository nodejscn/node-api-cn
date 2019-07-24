
以下是一些插件示例，用于帮助开发者入门。
这些例子使用了 V8 的 API。
查看在线的 [V8 文档]有助于了解各种 V8 调用，V8 的[嵌入器指南]解释了句柄、作用域和函数模板等的一些概念。

每个示例都使用以下的 `binding.gyp` 文件：

```json
{
  "targets": [
    {
      "target_name": "addon",
      "sources": [ "addon.cc" ]
    }
  ]
}
```

如果有一个以上的 `.cc` 文件，则只需添加额外的文件名到 `sources` 数组。
例如：

```json
"sources": ["addon.cc", "myexample.cc"]
```

当 `binding.gyp` 文件准备就绪，则插件示例可以使用 `node-gyp` 进行配置和构建：

```console
$ node-gyp configure build
```


