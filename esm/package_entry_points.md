
There are two fields that can define entry points for a package: `"main"` and
`"exports"`. The `"main"` field is supported in all versions of Node.js, but its
capabilities are limited: it only defines the main entry point of the package.
The `"exports"` field, part of [Package Exports][], provides an alternative to
`"main"` where the package main entry point can be defined while also
encapsulating the package, preventing any other entry points besides those
defined in `"exports"`. If package entry points are defined in both `"main"` and
`"exports"`, the latter takes precedence in versions of Node.js that support
`"exports"`. [Conditional Exports][] can also be used within `"exports"` to
define different package entry points per environment.

