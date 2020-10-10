<!-- YAML
added: v10.0.0
-->
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
* 返回: {Promise}

[`filehandle.writeFile()`] 的别名。

当在文件句柄上进行操作时，无法将模式更改为使用 [`fsPromises.open()`] 设置的模式。 
因此，这等效于 [`filehandle.writeFile()`]。


