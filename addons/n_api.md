
> Stability: 1 - Experimental

N-API is an API for building native Addons. It is independent from
the underlying JavaScript runtime (ex V8) and is maintained as part of
Node.js itself. This API will be Application Binary Interface (ABI) stable
across version of Node.js. It is intended to insulate Addons from
changes in the underlying JavaScript engine and allow modules
compiled for one version to run on later versions of Node.js without
recompilation. Addons are built/packaged with the same approach/tools
outlined in this document (node-gyp, etc.). The only difference is the
set of APIs that are used by the native code. Instead of using the V8
or [Native Abstractions for Node.js][] APIs, the functions available
in the N-API are used.

The functions available and how to use them are documented in the
section titled [C/C++ Addons - N-API](n-api.html).

