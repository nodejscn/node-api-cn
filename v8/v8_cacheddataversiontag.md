<!-- YAML
added: v8.0.0
-->

* 返回: {integer}

返回一个整数，表示从 V8 版本、命令行标志、以及检测到的 CPU 特性派生的版本标记。 
这对于判断 [`vm.Script`] 的 `cachedData` buffer 是否与此 V8 实例兼容非常有用。

