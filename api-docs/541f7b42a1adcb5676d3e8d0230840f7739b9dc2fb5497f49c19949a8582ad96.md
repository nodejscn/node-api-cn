
Although N-API provides an ABI stability guarantee, other parts of Node.js do
not, and any external libraries used from the addon may not. In particular,
none of the following APIs provide an ABI stability guarantee across major
versions:
* the Node.js C++ APIs available via any of
    ```C++
    #include <node.h>
    #include <node_buffer.h>
    #include <node_version.h>
    #include <node_object_wrap.h>
    ```
* the libuv APIs which are also included with Node.js and available via
    ```C++
    #include <uv.h>
    ```
* the V8 API available via
    ```C++
    #include <v8.h>
    ```

Thus, for an addon to remain ABI-compatible across Node.js major versions, it
must make use exclusively of N-API by restricting itself to using
```C
#include <node_api.h>
```
and by checking, for all external libraries that it uses, that the external
library makes ABI stability guarantees similar to N-API.

