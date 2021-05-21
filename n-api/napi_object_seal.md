<!-- YAML
added:
  - v14.14.0
  - v12.20.0
napiVersion: 8
-->

```c
napi_status napi_object_seal(napi_env env,
                             napi_value object);
```

* `[in] env`: The environment that the Node-API call is invoked under.
* `[in] object`: The object to seal.

Returns `napi_ok` if the API succeeded.

This method seals a given object. This prevents new properties from being
added to it, as well as marking all existing properties as non-configurable.
This is described in [Section 19.1.2.20](https://tc39.es/ecma262/#sec-object.seal)
of the ECMA-262 specification.

