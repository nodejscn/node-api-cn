<!-- YAML
added: v0.9.12
-->

* {boolean}

`process.throwDeprecation` 的初始值表明是否在当前的 Node.js 进程上设置了 `--throw-deprecation` 标志。 
`process.throwDeprecation` 是可变的，因此可以在运行时设置废弃警告是否应该导致错误。 
有关更多信息，参见 [`'warning'` 事件][process_warning]和 [`emitWarning()` 方法][process_emit_warning] 的文档。

```console
$ node --throw-deprecation -p "process.throwDeprecation"
true
$ node -p "process.throwDeprecation"
undefined
$ node
> process.emitWarning('test', 'DeprecationWarning');
undefined
> (node:26598) DeprecationWarning: test
> process.throwDeprecation = true;
true
> process.emitWarning('test', 'DeprecationWarning');
抛出:
[DeprecationWarning: test] { name: 'DeprecationWarning' }
```


