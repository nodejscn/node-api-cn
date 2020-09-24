
N-API versions are additive and versioned independently from Node.js.
Version 4 is an extension to version 3 in that it has all of the APIs
from version 3 with some additions. This means that it is not necessary
to recompile for new versions of Node.js which are
listed as supporting a later version.

<!-- For accessibility purposes, this table needs row headers. That means we
     can't do it in markdown. Hence, the raw HTML. -->

<table>
  <tr>
    <td></td>
    <th scope="col">1</th>
    <th scope="col">2</th>
    <th scope="col">3</th>
    <th scope="col">4</th>
    <th scope="col">5</th>
    <th scope="col">6</th>
  </tr>
  <tr>
    <th scope="row">v6.x</th>
    <td></td>
    <td></td>
    <td>v6.14.2*</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th scope="row">v8.x</th>
    <td>v8.6.0**</td>
    <td>v8.10.0*</td>
    <td>v8.11.2</td>
    <td>v8.16.0</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th scope="row">v9.x</th>
    <td>v9.0.0*</td>
    <td>v9.3.0*</td>
    <td>v9.11.0*</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th scope="row">v10.x</th>
    <td>v10.0.0</td>
    <td>v10.0.0</td>
    <td>v10.0.0</td>
    <td>v10.16.0</td>
    <td>v10.17.0</td>
    <td>v10.20.0</td>
  </tr>
  <tr>
    <th scope="row">v11.x</th>
    <td>v11.0.0</td>
    <td>v11.0.0</td>
    <td>v11.0.0</td>
    <td>v11.8.0</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th scope="row">v12.x</th>
    <td>v12.0.0</td>
    <td>v12.0.0</td>
    <td>v12.0.0</td>
    <td>v12.0.0</td>
    <td>v12.11.0</td>
    <td>v12.17.0</td>
  </tr>
  <tr>
    <th scope="row">v13.x</th>
    <td>v13.0.0</td>
    <td>v13.0.0</td>
    <td>v13.0.0</td>
    <td>v13.0.0</td>
    <td>v13.0.0</td>
    <td></td>
  </tr>
  <tr>
    <th scope="row">v14.x</th>
    <td>v14.0.0</td>
    <td>v14.0.0</td>
    <td>v14.0.0</td>
    <td>v14.0.0</td>
    <td>v14.0.0</td>
    <td>v14.0.0</td>
  </tr>
</table>

\* N-API was experimental.

\*\* Node.js 8.0.0 included N-API as experimental. It was released as N-API
version 1 but continued to evolve until Node.js 8.6.0. The API is different in
versions prior to Node.js 8.6.0. We recommend N-API version 3 or later.

Each API documented for N-API will have a header named `added in:`, and APIs
which are stable will have the additional header `N-API version:`.
APIs are directly usable when using a Node.js version which supports
the N-API version shown in `N-API version:` or higher.
When using a Node.js version that does not support the
`N-API version:` listed or if there is no `N-API version:` listed,
then the API will only be available if
`#define NAPI_EXPERIMENTAL` precedes the inclusion of `node_api.h`
or `js_native_api.h`. If an API appears not to be available on
a version of Node.js which is later than the one shown in `added in:` then
this is most likely the reason for the apparent absence.

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

```c
// addon.h
#ifndef _ADDON_H_
#define _ADDON_H_
#include <js_native_api.h>
napi_value create_addon(napi_env env);
#endif  // _ADDON_H_
```

```c
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

```c
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

