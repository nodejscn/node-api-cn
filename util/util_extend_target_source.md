<!-- YAML
added: v0.7.5
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`Object.assign()`] instead.

The `util._extend()` method was never intended to be used outside of internal
Node.js modules. The community found and used it anyway.

It is deprecated and should not be used in new code. JavaScript comes with very
similar built-in functionality through [`Object.assign()`].

[`Array.isArray`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray
[constructor]: https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object/constructor
[semantically incompatible]: https://github.com/nodejs/node/issues/4179
[`util.inspect()`]: #util_util_inspect_object_options
[Customizing `util.inspect` colors]: #util_customizing_util_inspect_colors
[Custom inspection functions on Objects]: #util_custom_inspection_functions_on_objects
[`Error`]: errors.html#errors_class_error
[`console.log()`]: console.html#console_console_log_data_args
[`console.error()`]: console.html#console_console_error_data_args
[`Buffer.isBuffer()`]: buffer.html#buffer_class_method_buffer_isbuffer_obj
[`Object.assign()`]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
