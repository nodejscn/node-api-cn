<!-- YAML
added:
 - v13.7.0
 - v10.20.0
napiVersion: 6
-->

```C
typedef enum {
  napi_key_include_prototypes,
  napi_key_own_only
} napi_key_collection_mode;
```

Describes the `Keys/Properties` filter enums:

`napi_key_collection_mode` limits the range of collected properties.

`napi_key_own_only` limits the collected properties to the given
object only. `napi_key_include_prototypes` will include all keys
of the objects's prototype chain as well.

