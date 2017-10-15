<!-- YAML
added: v0.9.1
-->

* Returns: {net.Server}

如果这个server在事件系统中是唯一有效的，那么对server调用`unref`将允许程序退出。如果这个server已经调用过`unref`那么再次调用将不会再有效果。
