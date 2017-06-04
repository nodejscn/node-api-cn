<!-- YAML
added: v0.6.9
-->

* `multicastAddress` {string}
* `multicastInterface` {string}, 可选的

通知内核将`multicastAddress`和`multicastInterface`提供的多路传送集合通过`IP_ADD_MEMBERSHIP`这个 socket 选项结合起来。若`multicastInterface`参数未指定，操作系统将会选择一个接口并向其添加成员。要为所有可用的接口添加成员，可以在每个接口上调用一次`addMembership`方法。

