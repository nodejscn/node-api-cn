<!-- YAML
added: v8.0.0
-->

销毁流，并且触发`error`事件。然后，可读流将释放所有的内部资源。

开发者不应该覆盖这个方法，应该使用[`readable._destroy`][readable-_destroy]方法。

