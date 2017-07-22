<!-- YAML
added: v0.7.1
-->

* `settings` {Object}

Emitted every time `.setupMaster()` is called.

每当 `.setupMaster()`  被调用的时候触发。

`settings` 对象是 `setupMaster()` 被调用时的 `cluster.settings` 对象，并且只能查询，因为在一个 tick 内 `.setupMaster()` 可以被调用多次。

如果精确度十分重要，请使用 `cluster.settings`。
