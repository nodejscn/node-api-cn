<!-- YAML
added: v0.1.101
-->
* `obj` {any}
* `options` {Object}
  * `showHidden` {boolean}
  * `depth` {number}
  * `colors` {boolean}

在 `obj` 上使用 [`util.inspect()`] 并打印结果字符串到 `stdout`。
该函数会绕过任何定义在 `obj` 上的自定义的 `inspect()` 函数。
可选的 `options` 对象可以传入用于改变被格式化的字符串：

- `showHidden` - 如果为 `true`，则该对象中的不可枚举属性和 symbol 属性也会显示。默认为 `false`。

- `depth` - 告诉 [`util.inspect()`] 函数当格式化对象时要递归多少次。
这对于检查较大的复杂对象很有用。
默认为 `2`。
设为 `null` 可无限递归。

- `colors` - 如果为 `true`，则输出会带有 ANSI 颜色代码。
默认为 `false`。
颜色是可定制的，详见[定制 `util.inspect()` 颜色]。

