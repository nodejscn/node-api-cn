<!-- YAML
added: v0.6.9
-->

* `multicastAddress` {string}
* `multicastInterface` {string}, 可选的

引导内核通过`IP_DROP_MEMBERSHIP`这个 socket 选项删除`multicastAddress`指定的多路传送集合。当 socket 被关闭或进程被终止时，该方法会被内核自动调用，所以大多数的应用都不用自行调用该方法。

若`multicastInterface`未指定，操作系统会尝试删除所有可用接口上的成员。

