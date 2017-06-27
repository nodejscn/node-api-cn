<!-- YAML
added: v0.1.17
-->

`process.mainModule`属性提供了一种获取[`require.main`][]的替代方式。
The difference is that if the main module changes at
runtime, [`require.main`][] may still refer to the original main module in modules
that were required before the change occurred.
一般来说，假定[`require.main`][]和`process.mainModule`引用相同的模块是安全的。

就像[`require.main`][]一样，如果没有入口脚本，`process.mainModule`的值是`undefined`。

