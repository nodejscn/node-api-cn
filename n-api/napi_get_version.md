<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status napi_get_version(napi_env env,
                                         uint32_t* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[out] result`: The highest version of N-API supported.

Returns `napi_ok` if the API succeeded.

This API returns the highest N-API version supported by the
Node.js runtime.  N-API is planned to be additive such that
newer releases of Node.js may support additional API functions.
In order to allow an addon to use a newer function when running with
versions of Node.js that support it, while providing
fallback behavior when running with Node.js versions that don't
support it:

* Call `napi_get_version()` to determine if the API is available.
* If available, dynamically load a pointer to the function using `uv_dlsym()`.
* Use the dynamically loaded pointer to invoke the function.
* If the function is not available, provide an alternate implementation
  that does not use the function.

<!-- it's very convenient to have all the anchors indexed -->
<!--lint disable no-unused-definitions remark-lint-->
[Asynchronous Operations]: #n_api_asynchronous_operations
[Basic N-API Data Types]: #n_api_basic_n_api_data_types
[ECMAScript Language Specification]: https://tc39.github.io/ecma262/
[Error Handling]: #n_api_error_handling
[Module Registration]: #n_api_module_registration
[Native Abstractions for Node.js]: https://github.com/nodejs/nan
[Object Lifetime Management]: #n_api_object_lifetime_management
[Object Wrap]: #n_api_object_wrap
[Section 9.1.6]: https://tc39.github.io/ecma262/#sec-ordinary-object-internal-methods-and-internal-slots-defineownproperty-p-desc
[Section 12.5.5]: https://tc39.github.io/ecma262/#sec-typeof-operator
[Section 24.3]: https://tc39.github.io/ecma262/#sec-dataview-objects
[Working with JavaScript Functions]: #n_api_working_with_javascript_functions
[Working with JavaScript Properties]: #n_api_working_with_javascript_properties
[Working with JavaScript Values]: #n_api_working_with_javascript_values
[Working with JavaScript Values - Abstract Operations]: #n_api_working_with_javascript_values_abstract_operations

[`napi_cancel_async_work`]: #n_api_napi_cancel_async_work
[`napi_close_escapable_handle_scope`]: #n_api_napi_close_escapable_handle_scope
[`napi_close_handle_scope`]: #n_api_napi_close_handle_scope
[`napi_create_async_work`]: #n_api_napi_create_async_work
[`napi_create_error`]: #n_api_napi_create_error
[`napi_create_external_arraybuffer`]: #n_api_napi_create_external_arraybuffer
[`napi_create_range_error`]: #n_api_napi_create_range_error
[`napi_create_reference`]: #n_api_napi_create_reference
[`napi_create_type_error`]: #n_api_napi_create_type_error
[`napi_delete_async_work`]: #n_api_napi_delete_async_work
[`napi_define_class`]: #n_api_napi_define_class
[`napi_delete_element`]: #n_api_napi_delete_element
[`napi_delete_property`]: #n_api_napi_delete_property
[`napi_delete_reference`]: #n_api_napi_delete_reference
[`napi_escape_handle`]: #n_api_napi_escape_handle
[`napi_get_array_length`]: #n_api_napi_get_array_length
[`napi_get_element`]: #n_api_napi_get_element
[`napi_get_property`]: #n_api_napi_get_property
[`napi_has_property`]: #n_api_napi_has_property
[`napi_has_own_property`]: #n_api_napi_has_own_property
[`napi_set_property`]: #n_api_napi_set_property
[`napi_get_reference_value`]: #n_api_napi_get_reference_value
[`napi_is_error`]: #n_api_napi_is_error
[`napi_is_exception_pending`]: #n_api_napi_is_exception_pending
[`napi_get_last_error_info`]: #n_api_napi_get_last_error_info
[`napi_get_and_clear_last_exception`]: #n_api_napi_get_and_clear_last_exception
[`napi_make_callback`]: #n_api_napi_make_callback
[`napi_open_escapable_handle_scope`]: #n_api_napi_open_escapable_handle_scope
[`napi_open_handle_scope`]: #n_api_napi_open_handle_scope
[`napi_property_descriptor`]: #n_api_napi_property_descriptor
[`napi_queue_async_work`]: #n_api_napi_queue_async_work
[`napi_reference_ref`]: #n_api_napi_reference_ref
[`napi_reference_unref`]: #n_api_napi_reference_unref
[`napi_throw`]: #n_api_napi_throw
[`napi_throw_error`]: #n_api_napi_throw_error
[`napi_throw_range_error`]: #n_api_napi_throw_range_error
[`napi_throw_type_error`]: #n_api_napi_throw_type_error
[`napi_unwrap`]: #n_api_napi_unwrap
[`napi_wrap`]: #n_api_napi_wrap

[`process.release`]: process.html#process_process_release
