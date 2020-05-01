<!-- YAML
added:
 - v13.7.0
 - v10.20.0
napiVersion: 6
-->

```C
typedef enum {
  napi_key_keep_numbers,
  napi_key_numbers_to_strings
} napi_key_conversion;
```

`napi_key_numbers_to_strings` will convert integer indices to
strings. `napi_key_keep_numbers` will return numbers for integer
indices.

