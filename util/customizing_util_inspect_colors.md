
<!-- type=misc -->

可以通过 `util.inspect.styles` 和 `util.inspect.colors` 属性全局地自定义 `util.inspect` 的颜色输出（如果已启用）。

`util.inspect.styles` 是一个映射，关联一个样式名到一个 `util.inspect.colors` 颜色。

默认的样式与关联的颜色有：

* `bigint` - `yellow`
* `boolean` - `yellow`
* `date` - `magenta`
* `module` - `underline`
* `name` - (no styling)
* `null` - `bold`
* `number` - `yellow`
* `regexp` - `red`
* `special` - `cyan` (例如 `Proxies`)
* `string` - `green`
* `symbol` - `green`
* `undefined` - `grey`

颜色样式使用 ANSI 控制码，可能不是所有终端都支持。
要验证颜色支持，请使用 [`tty.hasColors()`]。

下面列出了预定义的控制代码（分为“修饰符”、“前景颜色”和“背景颜色”）。

