
When an application is using a package that provides both CommonJS and ES module
sources, there is a risk of certain bugs if both versions of the package get
loaded. This potential comes from the fact that the `pkgInstance` created by
`const pkgInstance = require('pkg')` is not the same as the `pkgInstance`
created by `import pkgInstance from 'pkg'` (or an alternative main path like
`'pkg/module'`). This is the “dual package hazard,” where two versions of the
same package can be loaded within the same runtime environment. While it is
unlikely that an application or package would intentionally load both versions
directly, it is common for an application to load one version while a dependency
of the application loads the other version. This hazard can happen because
Node.js supports intermixing CommonJS and ES modules, and can lead to unexpected
behavior.

If the package main export is a constructor, an `instanceof` comparison of
instances created by the two versions returns `false`, and if the export is an
object, properties added to one (like `pkgInstance.foo = 3`) are not present on
the other. This differs from how `import` and `require` statements work in
all-CommonJS or all-ES module environments, respectively, and therefore is
surprising to users. It also differs from the behavior users are familiar with
when using transpilation via tools like [Babel][] or [`esm`][].

