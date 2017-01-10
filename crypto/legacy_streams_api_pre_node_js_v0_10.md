
The Crypto module was added to Node.js before there was the concept of a
unified Stream API, and before there were [`Buffer`][] objects for handling
binary data. As such, the many of the `crypto` defined classes have methods not
typically found on other Node.js classes that implement the [streams][stream]
API (e.g. `update()`, `final()`, or `digest()`). Also, many methods accepted
and returned `'latin1'` encoded strings by default rather than Buffers. This
default was changed after Node.js v0.8 to use [`Buffer`][] objects by default
instead.

