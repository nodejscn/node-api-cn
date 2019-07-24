所有用Node.js所运行的JavaScript代码都是在一个“上下文”的作用域中被执行的。
根据[V8 Embedder's Guide][]：

> 在V8中，一个上下文是一个执行环境，它允许分离的，无关的JavaScript应用在一个V8的单例中被运行。
> 你必须明确地指定用于运行所有JavaScript代码的上下文。

当调用`vm.createContext()`时，传入的`sandbox`对象（或者新建的一个`sandbox`对象，若原`sandbox`为`undefined`)在底层会和一个新的V8上下文实例联系上。这个V8上下文在一个隔离的全局环境中，使用`vm`模块的方法运行`code`。创建V8上下文和使之联系上`sandbox`的过程在此文档中被称作为"上下文隔离化"`sandbox`。

[`Error`]: errors.html#errors_class_error
[`eval()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval
[`script.runInContext()`]: #vm_script_runincontext_contextifiedsandbox_options
[`script.runInThisContext()`]: #vm_script_runinthiscontext_options
[`vm.createContext()`]: #vm_vm_createcontext_sandbox
[`vm.runInContext()`]: #vm_vm_runincontext_code_contextifiedsandbox_options
[`vm.runInThisContext()`]: #vm_vm_runinthiscontext_code_options
[V8 Embedder's Guide]: https://github.com/v8/v8/wiki/Embedder's%20Guide#contexts
[command line option]: cli.html
[contextified]: #vm_what_does_it_mean_to_contextify_an_object
[global object]: https://es5.github.io/#x15.1
[indirect `eval()` call]: https://es5.github.io/#x10.4.2
