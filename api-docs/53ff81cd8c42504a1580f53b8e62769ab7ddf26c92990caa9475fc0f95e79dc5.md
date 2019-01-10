<!-- YAML
added: v0.1.17
-->

`process.mainModule`属性提供了一种获取[`require.main`][]的替代方式。
区别在于，若主模块在运行时中发生改变，
[`require.main`][]可能仍然指向变化之前所依赖的模块
一般来说，假定[`require.main`][]和`process.mainModule`引用相同的模块是安全的。

就像[`require.main`][]一样，如果没有入口脚本，`process.mainModule`的值是`undefined`。

