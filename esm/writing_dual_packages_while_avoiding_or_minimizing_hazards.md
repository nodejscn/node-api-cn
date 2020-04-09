
First, the hazard described in the previous section occurs when a package
contains both CommonJS and ES module sources and both sources are provided for
use in Node.js, either via separate main entry points or exported paths. A
package could instead be written where any version of Node.js receives only
CommonJS sources, and any separate ES module sources the package may contain
could be intended only for other environments such as browsers. Such a package
would be usable by any version of Node.js, since `import` can refer to CommonJS
files; but it would not provide any of the advantages of using ES module syntax.

A package could also switch from CommonJS to ES module syntax in a breaking
change version bump. This has the disadvantage that the newest version
of the package would only be usable in ES module-supporting versions of Node.js.

Every pattern has tradeoffs, but there are two broad approaches that satisfy the
following conditions:

1. The package is usable via both `require` and `import`.
1. The package is usable in both current Node.js and older versions of Node.js
   that lack support for ES modules.
1. The package main entry point, e.g. `'pkg'` can be used by both `require` to
   resolve to a CommonJS file and by `import` to resolve to an ES module file.
   (And likewise for exported paths, e.g. `'pkg/feature'`.)
1. The package provides named exports, e.g. `import { name } from 'pkg'` rather
   than `import pkg from 'pkg'; pkg.name`.
1. The package is potentially usable in other ES module environments such as
   browsers.
1. The hazards described in the previous section are avoided or minimized.

