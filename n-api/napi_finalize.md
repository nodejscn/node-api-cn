<!-- YAML
added: v8.0.0
napiVersion: 1
-->
Function pointer type for add-on provided functions that allow the user to be
notified when externally-owned data is ready to be cleaned up because the
object with which it was associated with, has been garbage-collected. The user
must provide a function satisfying the following signature which would get
called upon the object's collection. Currently, `napi_finalize` can be used for
finding out when objects that have external data are collected.

```c
typedef void (*napi_finalize)(napi_env env,
                              void* finalize_data,
                              void* finalize_hint);
```

Unless for reasons discussed in [Object Lifetime Management][], creating a
handle and/or callback scope inside the function body is not necessary.

