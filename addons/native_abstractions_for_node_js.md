
Each of the examples illustrated in this document make direct use of the
Node.js and V8 APIs for implementing Addons. It is important to understand
that the V8 API can, and has, changed dramatically from one V8 release to the
next (and one major Node.js release to the next). With each change, Addons may
need to be updated and recompiled in order to continue functioning. The Node.js
release schedule is designed to minimize the frequency and impact of such
changes but there is little that Node.js can do currently to ensure stability
of the V8 APIs.

The [Native Abstractions for Node.js][] (or `nan`) provide a set of tools that
Addon developers are recommended to use to keep compatibility between past and
future releases of V8 and Node.js. See the `nan` [examples][] for an
illustration of how it can be used.

