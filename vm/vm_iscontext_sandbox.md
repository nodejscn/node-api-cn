<!-- YAML
added: v0.11.7
-->

* `sandbox` {Object}

Returns `true` if the given `sandbox` object has been [contextified][] using
[`vm.createContext()`][].

当给定的`sandbox`对象已经被[`vm.createContext()`][]上下文隔离化，则返回真。
