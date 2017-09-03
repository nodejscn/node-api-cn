<!-- YAML
added: v0.1.16
-->

`exports` 变量是在模块的文件级别作用域内有效的，它在模块被执行前被赋予 `module.exports` 的值。

它有一个快捷方式，以便 `module.exports.f = ...` 可以被更简洁地写成 `exports.f = ...`。
注意，就像任何变量，如果一个新的值被赋值给 `exports`，它就不再绑定到 `module.exports`：

```js
module.exports.hello = true; // 从对模块的引用中导出
exports = { hello: false };  // 不导出，只在模块内有效
```

当 `module.exports` 属性被一个新的对象完全替代时，也会重新赋值 `exports`，例如：

<!-- eslint-disable func-name-matching -->
```js
module.exports = exports = function Constructor() {
  // ... 及其他
};
```

为了解释这个行为，想象对 `require()` 的假设实现，它跟 `require()` 的实际实现相当类似：

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

