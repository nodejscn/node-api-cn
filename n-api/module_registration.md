N-API modules are registered in a manner similar to other modules
except that instead of using the `NODE_MODULE` macro the following
is used:

```C
NAPI_MODULE(NODE_GYP_MODULE_NAME, Init)
```

The next difference is the signature for the `Init` method. For a N-API
module it is as follows:

```C
napi_value Init(napi_env env, napi_value exports);
```

The return value from `Init` is treated as the `exports` object for the module.
The `Init` method is passed an empty object via the `exports` parameter as a
convenience. If `Init` returns NULL, the parameter passed as `exports` is
exported by the module. N-API modules cannot modify the `module` object but can
specify anything as the `exports` property of the module.

For example, to add the method `hello` as a function so that it can be called
as a method provided by the addon:

```C
napi_value Init(napi_env env, napi_value exports) {
  napi_status status;
  napi_property_descriptor desc =
    {"hello", Method, 0, 0, 0, napi_default, 0};
  if (status != napi_ok) return nullptr;
  status = napi_define_properties(env, exports, 1, &desc);
  if (status != napi_ok) return nullptr;
  return exports;
}
```

For example, to set a function to be returned by the `require()` for the addon:

```C
napi_value Init(napi_env env, napi_value exports) {
  napi_value method;
  napi_status status;
  status = napi_create_function(env, "exports", Method, NULL, &method));
  if (status != napi_ok) return nullptr;
  return method;
}
```

For example, to define a class so that new instances can be created
(often used with [Object Wrap][]):

```C
// NOTE: partial example, not all referenced code is included
napi_value Init(napi_env env, napi_value exports) {
  napi_status status;
  napi_property_descriptor properties[] = {
    { "value", nullptr, GetValue, SetValue, 0, napi_default, 0 },
    DECLARE_NAPI_METHOD("plusOne", PlusOne),
    DECLARE_NAPI_METHOD("multiply", Multiply),
  };

  napi_value cons;
  status =
      napi_define_class(env, "MyObject", New, nullptr, 3, properties, &cons);
  if (status != napi_ok) return nullptr;

  status = napi_create_reference(env, cons, 1, &constructor);
  if (status != napi_ok) return nullptr;

  status = napi_set_named_property(env, exports, "MyObject", cons);
  if (status != napi_ok) return nullptr;

  return exports;
}
```

For more details on setting properties on objects, see the section on
[Working with JavaScript Properties][].

For more details on building addon modules in general, refer to the existing API

