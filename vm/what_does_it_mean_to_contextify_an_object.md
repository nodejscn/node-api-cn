
All JavaScript executed within Node.js runs within the scope of a "context".
According to the [V8 Embedder's Guide][]:

> In V8, a context is an execution environment that allows separate, unrelated,
> JavaScript applications to run in a single instance of V8. You must explicitly
> specify the context in which you want any JavaScript code to be run.

When the method `vm.createContext()` is called, the `sandbox` object that is
passed in (or a newly created object if `sandbox` is `undefined`) is associated
internally with a new instance of a V8 Context. This V8 Context provides the
`code` run using the `vm` module's methods with an isolated global environment
within which it can operate. The process of creating the V8 Context and
associating it with the `sandbox` object is what this document refers to as
"contextifying" the `sandbox`.

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
