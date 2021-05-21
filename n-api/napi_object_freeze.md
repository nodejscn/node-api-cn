<!-- YAML
added:
  - v14.14.0
  - v12.20.0
napiVersion: 8
-->

```c
napi_status napi_object_freeze(napi_env env,
                               napi_value object);
```

* `[in] env`: The environment that the Node-API call is invoked under.
* `[in] object`: The object to freeze.

Returns `napi_ok` if the API succeeded.

This method freezes a given object. This prevents new properties from
being added to it, existing properties from being removed, prevents
changing the enumerability, configurability, or writability of existing
properties, and prevents the values of existing properties from being changed.
It also prevents the object's prototype from being changed. This is described
in [Section 19.1.2.6](https://tc39.es/ecma262/#sec-object.freeze) of the
ECMA-262 specification.

