
> Stability: 1 - Experimental

Conditional exports provide a way to map to different paths depending on
certain conditions. They are supported for both CommonJS and ES module imports.

For example, a package that wants to provide different ES module exports for
`require()` and `import` can be written:

```json
// package.json
{
  "main": "./main-require.cjs",
  "exports": {
    "import": "./main-module.js",
    "require": "./main-require.cjs"
  },
  "type": "module"
}
```

Node.js supports the following conditions out of the box:

* `"import"` - matched when the package is loaded via `import` or
   `import()`, or via any top-level import or resolve operation by the
   ECMAScript module loader. Applies regardless of the module format of the
   target file. _Always mutually exclusive with `"require"`._
* `"require"` - matched when the package is loaded via `require()`. The
   referenced file should be loadable with `require()` although the condition
   will be matched regardless of the module format of the target file. Expected
   formats include CommonJS, JSON, and native addons but not ES modules as
   `require()` doesn't support them. _Always mutually exclusive with
   `"import"`._
* `"node"` - matched for any Node.js environment. Can be a CommonJS or ES
   module file. _This condition should always come after `"import"` or
   `"require"`._
* `"default"` - the generic fallback that will always match. Can be a CommonJS
   or ES module file. _This condition should always come last._

Within the [`"exports"`][] object, key order is significant. During condition
matching, earlier entries have higher priority and take precedence over later
entries. _The general rule is that conditions should be from most specific to
least specific in object order_.

Other conditions such as `"browser"`, `"electron"`, `"deno"`, `"react-native"`,
etc. are unknown to, and thus ignored by Node.js. Runtimes or tools other than
Node.js may use them at their discretion. Further restrictions, definitions, or
guidance on condition names may occur in the future.

Using the `"import"` and `"require"` conditions can lead to some hazards,
which are further explained in [the dual CommonJS/ES module packages section][].

Conditional exports can also be extended to exports subpaths, for example:

```json
{
  "main": "./main.js",
  "exports": {
    ".": "./main.js",
    "./feature": {
      "node": "./feature-node.js",
      "default": "./feature.js"
    }
  }
}
```

Defines a package where `require('pkg/feature')` and `import 'pkg/feature'`
could provide different implementations between Node.js and other JS
environments.

When using environment branches, always include a `"default"` condition where
possible. Providing a `"default"` condition ensures that any unknown JS
environments are able to use this universal implementation, which helps avoid
these JS environments from having to pretend to be existing environments in
order to support packages with conditional exports. For this reason, using
`"node"` and `"default"` condition branches is usually preferable to using
`"node"` and `"browser"` condition branches.

