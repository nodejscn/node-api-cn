Node-API modules are registered in a manner similar to other modules
except that instead of using the `NODE_MODULE` macro the following
is used:

```c
NAPI_MODULE(NODE_GYP_MODULE_NAME, Init)
```

The next difference is the signature for the `Init` method. For a Node-API
module it is as follows:

```c
napi_value Init(napi_env env, napi_value exports);
```

The return value from `Init` is treated as the `exports` object for the module.
The `Init` method is passed an empty object via the `exports` parameter as a
convenience. If `Init` returns `NULL`, the parameter passed as `exports` is
exported by the module. Node-API modules cannot modify the `module` object but
can specify anything as the `exports` property of the module.

To add the method `hello` as a function so that it can be called as a method
provided by the addon:

```c
napi_value Init(napi_env env, napi_value exports) {
  napi_status status;
  napi_property_descriptor desc = {
    "hello",
    NULL,
    Method,
    NULL,
    NULL,
    NULL,
    napi_writable | napi_enumerable | napi_configurable,
    NULL
  };
  status = napi_define_properties(env, exports, 1, &desc);
  if (status != napi_ok) return NULL;
  return exports;
}
```

To set a function to be returned by the `require()` for the addon:

```c
napi_value Init(napi_env env, napi_value exports) {
  napi_value method;
  napi_status status;
  status = napi_create_function(env, "exports", NAPI_AUTO_LENGTH, Method, NULL, &method);
  if (status != napi_ok) return NULL;
  return method;
}
```

To define a class so that new instances can be created (often used with
[Object wrap][]):

```c
// NOTE: partial example, not all referenced code is included
napi_value Init(napi_env env, napi_value exports) {
  napi_status status;
  napi_property_descriptor properties[] = {
    { "value", NULL, NULL, GetValue, SetValue, NULL, napi_writable | napi_configurable, NULL },
    DECLARE_NAPI_METHOD("plusOne", PlusOne),
    DECLARE_NAPI_METHOD("multiply", Multiply),
  };

  napi_value cons;
  status =
      napi_define_class(env, "MyObject", New, NULL, 3, properties, &cons);
  if (status != napi_ok) return NULL;

  status = napi_create_reference(env, cons, 1, &constructor);
  if (status != napi_ok) return NULL;

  status = napi_set_named_property(env, exports, "MyObject", cons);
  if (status != napi_ok) return NULL;

  return exports;
}
```

You can also use the `NAPI_MODULE_INIT` macro, which acts as a shorthand
for `NAPI_MODULE` and defining an `Init` function:

```c
NAPI_MODULE_INIT() {
  napi_value answer;
  napi_status result;

  status = napi_create_int64(env, 42, &answer);
  if (status != napi_ok) return NULL;

  status = napi_set_named_property(env, exports, "answer", answer);
  if (status != napi_ok) return NULL;

  return exports;
}
```

All Node-API addons are context-aware, meaning they may be loaded multiple
times. There are a few design considerations when declaring such a module.
The documentation on [context-aware addons][] provides more details.

The variables `env` and `exports` will be available inside the function body
following the macro invocation.

For more details on setting properties on objects, see the section on
[Working with JavaScript properties][].

For more details on building addon modules in general, refer to the existing
API.

