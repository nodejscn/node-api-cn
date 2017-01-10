
Node.js Addons are dynamically-linked shared objects, written in C or C++, that
can be loaded into Node.js using the [`require()`][require] function, and used
just as if they were an ordinary Node.js module. They are used primarily to
provide an interface between JavaScript running in Node.js and C/C++ libraries.

At the moment, the method for implementing Addons is rather complicated,
involving knowledge of several components and APIs :

 - V8: the C++ library Node.js currently uses to provide the
   JavaScript implementation. V8 provides the mechanisms for creating objects,
   calling functions, etc. V8's API is documented mostly in the
   `v8.h` header file (`deps/v8/include/v8.h` in the Node.js source
   tree), which is also available [online][v8-docs].

 - [libuv][]: The C library that implements the Node.js event loop, its worker
   threads and all of the asynchronous behaviors of the platform. It also
   serves as a cross-platform abstraction library, giving easy, POSIX-like
   access across all major operating systems to many common system tasks, such
   as interacting with the filesystem, sockets, timers and system events. libuv
   also provides a pthreads-like threading abstraction that may be used to
   power more sophisticated asynchronous Addons that need to move beyond the
   standard event loop. Addon authors are encouraged to think about how to
   avoid blocking the event loop with I/O or other time-intensive tasks by
   off-loading work via libuv to non-blocking system operations, worker threads
   or a custom use of libuv's threads.

 - Internal Node.js libraries. Node.js itself exports a number of C/C++ APIs
   that Addons can use &mdash; the most important of which is the
   `node::ObjectWrap` class.

 - Node.js includes a number of other statically linked libraries including
   OpenSSL. These other libraries are located in the `deps/` directory in the
   Node.js source tree. Only the V8 and OpenSSL symbols are purposefully
   re-exported by Node.js and may be used to various extents by Addons.
   See [Linking to Node.js' own dependencies][] for additional information.

All of the following examples are available for [download][] and may
be used as a starting-point for your own Addon.

