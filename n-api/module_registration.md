N-API modules are registered in the same manner as other modules
except that instead of using the `NODE_MODULE` macro the following
is used:

```C
NAPI_MODULE(addon, Init)
```

The next difference is the signature for the `Init` method. For a N-API
module it is as follows:

```C
void Init(napi_env env, napi_value exports, napi_value module, void* priv);
```

As with any other module, functions are exported by either adding them to
the `exports` or `module` objects passed to the `Init` method.

For example, to add the method `hello` as a function so that it can be called
as a method provided by the addon:

```C
void Init(napi_env env, napi_value exports, napi_value module, void* priv) {
  napi_status status;
  napi_property_descriptor desc =
    {"hello", Method, 0, 0, 0, napi_default, 0};
  status = napi_define_properties(env, exports, 1, &desc);
}
```

For example, to set a function to be returned by the `require()` for the addon:

```C
void Init(napi_env env, napi_value exports, napi_value module, void* priv) {
  napi_status status;
  napi_property_descriptor desc =
    {"exports", Method, 0, 0, 0, napi_default, 0};
  status = napi_define_properties(env, module, 1, &desc);
}
```

For example, to define a class so that new instances can be created
(often used with [Object Wrap][]):

```C
// NOTE: partial example, not all referenced code is included

napi_status status;
napi_property_descriptor properties[] = {
    { "value", nullptr, GetValue, SetValue, 0, napi_default, 0 },
    DECLARE_NAPI_METHOD("plusOne", PlusOne),
    DECLARE_NAPI_METHOD("multiply", Multiply),
};

napi_value cons;
status =
    napi_define_class(env, "MyObject", New, nullptr, 3, properties, &cons);
if (status != napi_ok) return;

status = napi_create_reference(env, cons, 1, &constructor);
if (status != napi_ok) return;

status = napi_set_named_property(env, exports, "MyObject", cons);
if (status != napi_ok) return;
```

For more details on setting properties on either the `exports` or `module`
objects, see the section on
[Working with JavaScript Properties][].

For more details on building addon modules in general, refer to the existing API

