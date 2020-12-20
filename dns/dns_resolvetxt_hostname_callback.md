<!-- YAML
added: v0.1.27
-->

<!--lint disable no-undefined-references list-item-bullet-indent-->
* `hostname` {string}
* `callback` {Function}
  * `err` {Error}
  * `records` [<string[][]>][_type_string_array_array]
<!--lint enable no-undefined-references list-item-bullet-indent-->

使用 DNS 协议为 `hostname` 解析文本查询（`TXT` 记录）。
传给 `callback` 函数的 `records` 参数是一个具有用于 `hostname` 的可用的文本记录的二维数组(例如：`[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]`)。
每个子数组包含一条 TXT 记录块。
根据用例，这些可以是连接在一起或单独对待。
