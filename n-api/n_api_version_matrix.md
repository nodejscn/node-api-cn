
N-API versions are additive and versioned independently from Node.js.
Version 4 is an extension to version 3 in that it has all of the APIs
from version 3 with some additions. This means that you
do not need to recompile for new versions of Node.js which are
listed as supporting a later version.

|       | 1       | 2        | 3        | 4        |
|:-----:|:-------:|:--------:|:--------:|:--------:|
| v6.x  |         |          | v6.14.2* |          |
| v8.x  | v8.0.0* | v8.10.0* | v8.11.2  | v8.16.0  |
| v9.x  | v9.0.0* | v9.3.0*  | v9.11.0* |          |
| v10.x |         |          | v10.0.0  |          |
| v11.x |         |          | v11.0.0  | v11.8.0  |
| v12.x |         |          |          | v12.0.0  |

\* Indicates that the N-API version was released as experimental

The N-APIs associated strictly with accessing ECMAScript features from native
code can be found separately in `js_native_api.h` and `js_native_api_types.h`.
The APIs defined in these headers are included in `node_api.h` and
`node_api_types.h`. The headers are structured in this way in order to allow
implementations of N-API outside of Node.js. For those implementations the
Node.js specific APIs may not be applicable.

The Node.js-specific parts of an addon can be separated from the code that
exposes the actual functionality to the JavaScript environment so that the
latter may be used with multiple implementations of N-API. In the example below,
`addon.c` and `addon.h` refer only to `js_native_api.h`. This ensures that
`addon.c` can be reused to compile against either the Node.js implementation of
N-API or any implementation of N-API outside of Node.js.

`addon_node.c` is a separate file that contains the Node.js specific entry point
to the addon and which instantiates the addon by calling into `addon.c` when the
addon is loaded into a Node.js environment.

```C
// addon.h
#ifndef _ADDON_H_
#define _ADDON_H_
#include <js_native_api.h>
napi_value create_addon(napi_env env);
#endif  // _ADDON_H_
```

```C
// addon.c
#include "addon.h"

#define NAPI_CALL(env, call)                                      \
  do {                                                            \
    napi_status status = (call);                                  \
    if (status != napi_ok) {                                      \
      const napi_extended_error_info* error_info = NULL;          \
      napi_get_last_error_info((env), &error_info);               \
      bool is_pending;                                            \
      napi_is_exception_pending((env), &is_pending);              \
      if (!is_pending) {                                          \
        const char* message = (error_info->error_message == NULL) \
            ? "empty error message"                               \
            : error_info->error_message;                          \
        napi_throw_error((env), NULL, message);                   \
        return NULL;                                              \
      }                                                           \
    }                                                             \
  } while(0)

static napi_value
DoSomethingUseful(napi_env env, napi_callback_info info) {
  // Do something useful.
  return NULL;
}

napi_value create_addon(napi_env env) {
  napi_value result;
  NAPI_CALL(env, napi_create_object(env, &result));

  napi_value exported_function;
  NAPI_CALL(env, napi_create_function(env,
                                      "doSomethingUseful",
                                      NAPI_AUTO_LENGTH,
                                      DoSomethingUseful,
                                      NULL,
                                      &exported_function));

  NAPI_CALL(env, napi_set_named_property(env,
                                         result,
                                         "doSomethingUseful",
                                         exported_function));

  return result;
}
```

```C
// addon_node.c
#include <node_api.h>
#include "addon.h"

NAPI_MODULE_INIT() {
  // This function body is expected to return a `napi_value`.
  // The variables `napi_env env` and `napi_value exports` may be used within
  // the body, as they are provided by the definition of `NAPI_MODULE_INIT()`.
  return create_addon(env);
}
```

