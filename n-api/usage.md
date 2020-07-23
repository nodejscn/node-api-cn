
In order to use the N-API functions, include the file [`node_api.h`][] which is
located in the src directory in the node development tree:

```c
#include <node_api.h>
```

This will opt into the default `NAPI_VERSION` for the given release of Node.js.
In order to ensure compatibility with specific versions of N-API, the version
can be specified explicitly when including the header:

```c
#define NAPI_VERSION 3
#include <node_api.h>
```

This restricts the N-API surface to just the functionality that was available in
the specified (and earlier) versions.

Some of the N-API surface is experimental and requires explicit opt-in:

```c
#define NAPI_EXPERIMENTAL
#include <node_api.h>
```

In this case the entire API surface, including any experimental APIs, will be
available to the module code.

