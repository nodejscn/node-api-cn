<!-- YAML
added: v9.10.0
napiVersion: 3
-->

```c
napi_status napi_fatal_exception(napi_env env, napi_value err);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] err`: The error that is passed to `'uncaughtException'`.

Trigger an `'uncaughtException'` in JavaScript. Useful if an async
callback throws an exception with no way to recover.

