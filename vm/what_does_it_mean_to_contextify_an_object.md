
所有用 Node.js 所运行的 JavaScript 代码都是在一个“上下文”的作用域中被执行的。
根据 [V8 嵌入式指南][V8 Embedder's Guide]：

> 在 V8 中，一个上下文是一个执行环境，它允许分离的，无关的 JavaScript 应用在一个 V8 的单例中被运行。
> 必须明确地指定用于运行所有 JavaScript 代码的上下文。

当调用 `vm.createContext()` 时，传入的 `sandbox` 对象（或者新建的一个 `sandbox` 对象，若原 `sandbox` 为 `undefined`）在底层会和一个新的V8上下文实例联系上。
这个 V8 上下文在一个隔离的全局环境中，使用 `vm` 模块的方法运行 `code`。
创建 V8 上下文和使之联系上 `sandbox` 的过程在此文档中被称作为"上下文隔离化" `sandbox`。

