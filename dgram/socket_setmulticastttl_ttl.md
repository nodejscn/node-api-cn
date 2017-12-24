<!-- YAML
added: v0.3.8
-->

* `ttl` {number} Integer

设置`IP_MULTICAST_TTL`套接字选项。
一般来说，TTL表示"生存时间"。这里特指一个IP数据包传输时允许的最大跳步数，尤其是对多播传输。
当IP数据包每向前经过一个路由或网关时，TTL值减1，若经过某个路由时，TTL值被减至0，便不再继续向前传输。

传给 `socket.setMulticastTTL()` 的参数是一个范围为0-255的跳步数。大多数系统的默认值是 `1` ，但是可以变化。

