
Prior to the introduction of support for ES modules in Node.js, it was a common
pattern for package authors to include both CommonJS and ES module JavaScript
sources in their package, with `package.json` `"main"` specifying the CommonJS
entry point and `package.json` `"module"` specifying the ES module entry point.
This enabled Node.js to run the CommonJS entry point while build tools such as
bundlers used the ES module entry point, since Node.js ignored (and still
ignores) `"module"`.

Node.js can now run ES module entry points, but it remains impossible for a
package to define separate CommonJS and ES module entry points. This is for good
reason: the `pkg` variable created from `import pkg from 'pkg'` is not the same
singleton as the `pkg` variable created from `const pkg = require('pkg')`, so if
both are referenced within the same app (including dependencies), unexpected
behavior might occur.

There are two general approaches to addressing this limitation while still
publishing a package that contains both CommonJS and ES module sources:

1. Document a new ES module entry point that’s not the package `"main"`, e.g.
   `import pkg from 'pkg/module.mjs'` (or `import 'pkg/esm'`, if using [package
   exports][]). The package `"main"` would still point to a CommonJS file, and
   thus the package would remain compatible with older versions of Node.js that
   lack support for ES modules.

1. Switch the package `"main"` entry point to an ES module file as part of a
   breaking change version bump. This version and above would only be usable on
   ES module-supporting versions of Node.js. If the package still contains a
   CommonJS version, it would be accessible via a path within the package, e.g.
   `require('pkg/commonjs')`; this is essentially the inverse of the previous
   approach. Package consumers who are using CommonJS-only versions of Node.js
   would need to update their code from `require('pkg')` to e.g.
   `require('pkg/commonjs')`.

Of course, a package could also include only CommonJS or only ES module sources.
An existing package could make a semver major bump to an ES module-only version,
that would only be supported in ES module-supporting versions of Node.js (and
other runtimes). New packages could be published containing only ES module
sources, and would be compatible only with ES module-supporting runtimes.

