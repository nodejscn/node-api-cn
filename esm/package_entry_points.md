
In a package’s `package.json` file, two fields can define entry points for a
package: `"main"` and `"exports"`. The `"main"` field is supported in all
versions of Node.js, but its capabilities are limited: it only defines the main
entry point of the package.

The `"exports"` field provides an alternative to `"main"` where the package
main entry point can be defined while also encapsulating the package, preventing
any other entry points besides those defined in `"exports"`. If package entry
points are defined in both `"main"` and `"exports"`, the latter takes precedence
in versions of Node.js that support `"exports"`. [Conditional Exports][] can
also be used within `"exports"` to define different package entry points per
environment, including whether the package is referenced via `require` or via
`import`.

If both `"exports"` and `"main"` are defined, the `"exports"` field takes
precedence over `"main"`.

Both `"main"` and `"exports"` entry points are not specific to ES modules or
CommonJS; `"main"` will be overridden by `"exports"` in a `require` so it is
not a CommonJS fallback.

This is important with regard to `require`, since `require` of ES module files
throws an error in all versions of Node.js. To create a package that works both
in modern Node.js via `import` and `require` and also legacy Node.js versions,
see [the dual CommonJS/ES module packages section][].

