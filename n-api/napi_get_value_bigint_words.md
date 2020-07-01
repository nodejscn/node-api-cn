<!-- YAML
added: v10.7.0
napiVersion: 6
-->

```c
napi_status napi_get_value_bigint_words(napi_env env,
                                        napi_value value,
                                        int* sign_bit,
                                        size_t* word_count,
                                        uint64_t* words);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: `napi_value` representing JavaScript `BigInt`.
* `[out] sign_bit`: Integer representing if the JavaScript `BigInt` is positive
   or negative.
* `[in/out] word_count`: Must be initialized to the length of the `words`
   array. Upon return, it will be set to the actual number of words that
   would be needed to store this `BigInt`.
* `[out] words`: Pointer to a pre-allocated 64-bit word array.

Returns `napi_ok` if the API succeeded.

This API converts a single `BigInt` value into a sign bit, 64-bit little-endian
array, and the number of elements in the array. `sign_bit` and `words` may be
both set to `NULL`, in order to get only `word_count`.

