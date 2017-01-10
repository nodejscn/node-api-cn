
Node.js uses a number of statically linked libraries such as V8, libuv and
OpenSSL. All Addons are required to link to V8 and may link to any of the
other dependencies as well. Typically, this is as simple as including
the appropriate `#include <...>` statements (e.g. `#include <v8.h>`) and
`node-gyp` will locate the appropriate headers automatically. However, there
are a few caveats to be aware of:

* When `node-gyp` runs, it will detect the specific release version of Node.js
and download either the full source tarball or just the headers. If the full
source is downloaded, Addons will have complete access to the full set of
Node.js dependencies. However, if only the Node.js headers are downloaded, then
only the symbols exported by Node.js will be available.

* `node-gyp` can be run using the `--nodedir` flag pointing at a local Node.js
source image. Using this option, the Addon will have access to the full set of
dependencies.

