<!-- YAML
added: v0.5.4
-->

* {Integer} **默认:** `50`

当调用 `buf.inspect()` 时返回的最大字节数。
可以被用户模块重写。
详见 [`util.inspect()`] 了解更多 `buf.inspect()` 的行为。

注意，这个属性是在通过 `require('buffer')` 返回的 `buffer` 模块上，而不是在 `Buffer` 的全局变量或 `Buffer` 实例上。

