<!-- YAML
added: v11.11.0
-->

```C
napi_status napi_get_date_value(napi_env env,
                                napi_value value,
                                double* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: `napi_value` representing a JavaScript `Date`.
* `[out] result`: Time value as a `double` represented as milliseconds
since midnight at the beginning of 01 January, 1970 UTC.

This API does not observe leap seconds; they are ignored, as
ECMAScript aligns with POSIX time specification.

Returns `napi_ok` if the API succeeded. If a non-date `napi_value` is passed
in it returns `napi_date_expected`.

This API returns the C double primitive of time value for the given JavaScript
`Date`.

