<!-- YAML
added: v0.5.4
-->

* {integer} **默认值:** `50`。

返回当调用 `buf.inspect()` 时将会返回的最大字节数。 
这可以被用户模块重写。 
有关 `buf.inspect()` 行为的更多详细信息，参阅 [`util.inspect()`]。

该属性是在 `require('buffer')` 返回的 `buffer` 模块上，而不是在 `Buffer` 全局变量或 `Buffer` 实例上。

