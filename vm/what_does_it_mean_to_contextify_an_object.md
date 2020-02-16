
所有用 Node.js 所运行的 JavaScript 代码都是在一个“上下文”的作用域中被执行的。
根据 [V8 嵌入式指南][V8 Embedder's Guide]：

> 在 V8 中，一个上下文是一个执行环境，它允许分离的，无关的 JavaScript 应用在一个 V8 的单例中被运行。
> 必须明确地指定用于运行所有 JavaScript 代码的上下文。

当调用 `vm.createContext()` 方法时，`contextObject`参数（如果 `contextObject` 为 `undefined`，则为新创建的对象）在内部与 V8 上下文的新实例相关联。 
该 V8 上下文提供了使用 `vm` 模块的方法运行的 `code` 以及可在其中运行的隔离的全局环境。 
创建 V8 上下文并将其与 `contextObject` 关联的过程是本文档所称的“上下文隔离化”对象。

