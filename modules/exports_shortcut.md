<!-- YAML
added: v0.1.16
-->

`exports` 变量是在一个模块的文件级作用域内可用的，并且在模块被执行之前被赋值 `module.exports` 的值。

它允许一个快捷方式，因此 `module.exports.f = ...` 可以被更简洁地写成 `exports.f = ...`。
但是，就像任何变量一样，如果一个新的值被赋值给 `exports`，则它不再被绑定到 `module.exports`：

```js
module.exports.hello = true; // 被从模块的 require 导出
exports = { hello: false };  // 不被导出，仅在模块中可用
```

当 `module.exports` 属性被一个新的对象完全地替换时，通常也重新赋值 `exports`：

<!-- eslint-disable func-name-matching -->
```js
module.exports = exports = function Constructor() {
  // ... 等
};
```

为了说明这种行为，想象 `require()` 假设的实现，这与 `require()` 实际完成的非常相似：

```js
function require(/* ... */) {
  const module = { exports: {} };
  ((module, exports) => {
    // 模块代码在这。在此示例中，定义一个函数。
    function someFunc() {}
    exports = someFunc;
    // 此时，exports 不再是 module.exports 的一个快捷方式，
    // 并且此模块仍然会导出一个空的默认对象。
    module.exports = someFunc;
    // 此时，该模块现在会导出 someFunc，而不是默认的对象。
  })(module, module.exports);
  return module.exports;
}
```

