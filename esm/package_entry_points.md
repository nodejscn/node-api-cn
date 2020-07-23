
In a package’s `package.json` file, two fields can define entry points for a
package: `"main"` and `"exports"`. The `"main"` field is supported in all
versions of Node.js, but its capabilities are limited: it only defines the main
entry point of the package.

The `"exports"` field provides an alternative to `"main"` where the package
main entry point can be defined while also encapsulating the package,
**preventing any other entry points besides those defined in `"exports"`**.
This encapsulation allows module authors to define a public interface for
their package.

If both `"exports"` and `"main"` are defined, the `"exports"` field takes
precedence over `"main"`. `"exports"` are not specific to ES modules or
CommonJS; `"main"` will be overridden by `"exports"` if it exists. As such
`"main"` cannot be used as a fallback for CommonJS but it can be used as a
fallback for legacy versions of Node.js that do not support the `"exports"`
field.

[Conditional exports][] can be used within `"exports"` to define different
package entry points per environment, including whether the package is
referenced via `require` or via `import`. For more information about supporting
both CommonJS and ES Modules in a single package please consult
[the dual CommonJS/ES module packages section][].

**Warning**: Introducing the `"exports"` field prevents consumers of a package
from using any entry points that are not defined, including the `package.json`
(e.g. `require('your-package/package.json')`. **This will likely be a breaking
change.**

To make the introduction of `"exports"` non-breaking, ensure that every
previously supported entry point is exported. It is best to explicitly specify
entry points so that the package’s public API is well-defined. For example,
a project that previous exported `main`, `lib`,
`feature`, and the `package.json` could use the following `package.exports`:

```json
{
  "name": "my-mod",
  "exports": {
    ".": "./lib/index.js",
    "./lib": "./lib/index.js",
    "./lib/index": "./lib/index.js",
    "./lib/index.js": "./lib/index.js",
    "./feature": "./feature/index.js",
    "./feature/index.js": "./feature/index.js",
    "./package.json": "./package.json"
  }
}
```

Alternatively a project could choose to export entire folders:

```json
{
  "name": "my-mod",
  "exports": {
    ".": "./lib/index.js",
    "./lib": "./lib/index.js",
    "./lib/": "./lib/",
    "./feature": "./feature/index.js",
    "./feature/": "./feature/",
    "./package.json": "./package.json"
  }
}
```

As a last resort, package encapsulation can be disabled entirely by creating an
export for the root of the package `"./": "./"`. This will expose every file in
the package at the cost of disabling the encapsulation and potential tooling
benefits this provides. As the ES Module loader in Node.js enforces the use of
[the full specifier path][], exporting the root rather than being explicit
about entry is less expressive than either of the prior examples. Not only
will encapsulation be lost but module consumers will be unable to
`import feature from 'my-mod/feature'` as they will need to provide the full
path `import feature from 'my-mod/feature/index.js`.

