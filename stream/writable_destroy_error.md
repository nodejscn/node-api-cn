<!-- YAML
added: v8.0.0
-->

* 返回: `this`

摧毁这个流，并发出传过来的错误。当这个函数被调用后，这个写入流就结束了。
使用者不应该重写这个函数，而是执行 [`writable._destroy`][writable-_destroy]。

