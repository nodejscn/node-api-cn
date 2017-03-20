<!-- YAML
added: v0.1.92
-->

允许/禁止keep-alive功能, 并且可选地在第一个keep-alive探针发送到空闲的socket上
之前，设置初始时延。
`enable`默认是`false`.

设置 `initialDelay`(毫秒)来设置在最后一个包收到之后和第一个keep-alive探针之前
的时延。设置初始时延为0将不改变默认设置的值。值默认为0.

返回 `socket`.

