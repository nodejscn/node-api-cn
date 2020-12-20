<!-- YAML
added: v8.0.0
-->

* 返回: {integer}

返回一个整数，表示从 V8 版本、命令行标志、以及检测到的 CPU 特性派生的版本标记。 
这对于判断 [`vm.Script`] 的 `cachedData` buffer 是否与此 V8 实例兼容非常有用。

```js
console.log(v8.cachedDataVersionTag()); // 3947234607
// The value returned by v8.cachedDataVersionTag() is derived from the V8
// version, command-line flags, and detected CPU features. Test that the value
// does indeed update when flags are toggled.
v8.setFlagsFromString('--allow_natives_syntax');
console.log(v8.cachedDataVersionTag()); // 183726201
```

