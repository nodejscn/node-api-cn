<!-- YAML
added: v10.0.0
-->

* `prefix` {string}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
* 返回: {Promise}

创建一个唯一的临时目录，且解决 `Promise` 时带上创建的目录路径。
唯一的目录名称是通过在提供的 `prefix` 的末尾附加六个随机字符来生成的。 
由于平台的不一致性，请避免在 `prefix` 中以 `X` 字符结尾。 
在某些平台上，特别是 BSD，可以返回六个以上的随机字符，并用随机字符替换 `prefix` 中结尾的 `X` 字符。

可选的 `options` 参数可以是指定字符编码的字符串，也可以是具有指定要使用的字符编码的 `encoding` 属性的对象。

```js
fsPromises.mkdtemp(path.join(os.tmpdir(), 'foo-'))
  .catch(console.error);
```

`fsPromises.mkdtemp()` 方法将六位随机选择的字符直接附加到 `prefix` 字符串。 
例如，给定目录 `/tmp`，如果打算在 `/tmp` 中创建临时目录，则 `prefix` 必须在尾部加上特定平台的路径分隔符（`require('path').sep`）。

