<!-- YAML
added: v10.7.0
napiVersion: 6
-->

```C
napi_status napi_create_bigint_words(napi_env env,
                                     int sign_bit,
                                     size_t word_count,
                                     const uint64_t* words,
                                     napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] sign_bit`: Determines if the resulting `BigInt` will be positive or
  negative.
* `[in] word_count`: The length of the `words` array.
* `[in] words`: An array of `uint64_t` little-endian 64-bit words.
* `[out] result`: A `napi_value` representing a JavaScript `BigInt`.

Returns `napi_ok` if the API succeeded.

This API converts an array of unsigned 64-bit words into a single `BigInt`
value.

The resulting `BigInt` is calculated as: (–1)<sup>`sign_bit`</sup> (`words[0]`
× (2<sup>64</sup>)<sup>0</sup> + `words[1]` × (2<sup>64</sup>)<sup>1</sup> + …)

