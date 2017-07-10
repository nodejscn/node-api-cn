<!-- YAML
added: v0.8.1
-->

* {boolean}

当该进程是主进程时，返回 true。这是由`process.env.NODE_UNIQUE_ID`决定的，当`process.env.NODE_UNIQUE_ID`为定义时，`isMaster`为`true`。

