
Prior to the introduction of support for ES modules in Node.js, it was a common
pattern for package authors to include both CommonJS and ES module JavaScript
sources in their package, with `package.json` [`"main"`][] specifying the
CommonJS entry point and `package.json` `"module"` specifying the ES module
entry point.
This enabled Node.js to run the CommonJS entry point while build tools such as
bundlers used the ES module entry point, since Node.js ignored (and still
ignores) the top-level `"module"` field.

Node.js can now run ES module entry points, and a package can contain both
CommonJS and ES module entry points (either via separate specifiers such as
`'pkg'` and `'pkg/es-module'`, or both at the same specifier via [Conditional
exports][]). Unlike in the scenario where `"module"` is only used by bundlers,
or ES module files are transpiled into CommonJS on the fly before evaluation by
Node.js, the files referenced by the ES module entry point are evaluated as ES
modules.

