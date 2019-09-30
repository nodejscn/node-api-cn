<!-- YAML
added: v11.11.0
-->

```C
napi_status napi_create_date(napi_env env,
                             double time,
                             napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] time`: ECMAScript time value in milliseconds since 01 January, 1970 UTC.
* `[out] result`: A `napi_value` representing a JavaScript `Date`.

Returns `napi_ok` if the API succeeded.

This API does not observe leap seconds; they are ignored, as
ECMAScript aligns with POSIX time specification.

This API allocates a JavaScript `Date` object.

JavaScript `Date` objects are described in
[Section 20.3][] of the ECMAScript Language Specification.

