<!-- YAML
added: v0.1.101
-->
* `obj` {any}
* `options` {Object} 
  * `showHidden` {boolean} 如果为 `true`，则也会显示对象的不可枚举属性和符号属性。**默认值:** `false`。
  * `depth` {number} 告诉 [`util.inspect()`] 格式化对象时要递归多少次。这对于检查大型复杂对象很有用。要使其无限递归，可传入 `null`。**默认值:** `2`。
  * `colors` {boolean} 如果为 `true`，则输出将使用 ANSI 颜色代码进行样式设置。颜色可定制，请参阅[自定义 `util.inspect()` 颜色][customizing `util.inspect()` colors]。**默认值:** `false`。

在 `obj` 上使用 [`util.inspect()`] 并将结果字符串打印到 `stdout`。 
此函数绕过 `obj` 上定义的任何自定义 `inspect()` 函数。


