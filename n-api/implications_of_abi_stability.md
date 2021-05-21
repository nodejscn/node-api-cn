
Although Node-API provides an ABI stability guarantee, other parts of Node.js do
not, and any external libraries used from the addon may not. In particular,
none of the following APIs provide an ABI stability guarantee across major
versions:

* the Node.js C++ APIs available via any of

    ```cpp
    #include <node.h>
    #include <node_buffer.h>
    #include <node_version.h>
    #include <node_object_wrap.h>
    ```

* the libuv APIs which are also included with Node.js and available via

    ```cpp
    #include <uv.h>
    ```

* the V8 API available via

    ```cpp
    #include <v8.h>
    ```

Thus, for an addon to remain ABI-compatible across Node.js major versions, it
must use Node-API exclusively by restricting itself to using

```c
#include <node_api.h>
```

and by checking, for all external libraries that it uses, that the external
library makes ABI stability guarantees similar to Node-API.

