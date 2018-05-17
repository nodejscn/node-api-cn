
<!--introduced_in=v7.7.0-->
<!-- type=misc -->

Node.js may deprecate APIs when either: (a) use of the API is considered to be
unsafe, (b) an improved alternative API has been made available, or (c)
breaking changes to the API are expected in a future major release.

Node.js utilizes three kinds of Deprecations:

* Documentation-only
* Runtime
* End-of-Life

A Documentation-only deprecation is one that is expressed only within the
Node.js API docs. These generate no side-effects while running Node.js.
Some Documentation-only deprecations trigger a runtime warning when launched
with [`--pending-deprecation`][] flag (or its alternative,
`NODE_PENDING_DEPRECATION=1` environment variable), similarly to Runtime
deprecations below. Documentation-only deprecations that support that flag
are explicitly labeled as such in the
[list of Deprecated APIs](#deprecations_list_of_deprecated_apis).

A Runtime deprecation will, by default, generate a process warning that will
be printed to `stderr` the first time the deprecated API is used. When the
`--throw-deprecation` command-line flag is used, a Runtime deprecation will
cause an error to be thrown.

An End-of-Life deprecation is used to identify code that either has been
removed or will soon be removed from Node.js.

