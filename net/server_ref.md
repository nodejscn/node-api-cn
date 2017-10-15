<!-- YAML
added: v0.9.1
-->

* Returns: {net.Server}

对应的是`unref`，如果server是唯一的，那么在`unref`之前调用`ref`将不会让程序退出（这是默认行为）。如果server已经调用过`ref`再次调用`ref`将不会再有效果。
