<!-- YAML
added: v0.1.16
-->

`exports` 变量是在模块的文件级作用域内可用的，且在模块执行之前赋值给 `module.exports`。

它允许使用快捷方式，因此 `module.exports.f = ...` 可以更简洁地写成 `exports.f = ...`。
但是，就像任何变量一样，如果为 `exports` 赋予了新值，则它将不再绑定到 `module.exports`：

```js
module.exports.hello = true; // 从模块的引用中导出。
exports = { hello: false };  // 不导出，仅在模块中可用。
```

当 `module.exports` 属性被新对象完全替换时，通常也会重新赋值 `exports`：

<!-- eslint-disable func-name-matching -->
```js
module.exports = exports = function Constructor() {
  // ... 
};
```

为了说明这种行为，想象对 `require()` 的假设实现，它与 `require()` 的实际实现非常类似：

```js
function require(/* ... */) {
  const module = { exports: {} };
  ((module, exports) => {
    // 模块代码在这。在这个例子中，定义了一个函数。
    function someFunc() {}
    exports = someFunc;
    // 此时，exports 不再是一个 module.exports 的快捷方式，
    // 且这个模块依然导出一个空的默认对象。
    module.exports = someFunc;
    // 此时，该模块导出 someFunc，而不是默认对象。
  })(module, module.exports);
  return module.exports;
}
```

