
Conditional exports provide a way to map to different paths depending on
certain conditions. They are supported for both CommonJS and ES module imports.

For example, a package that wants to provide different ES module exports for
Node.js and the browser can be written:

<!-- eslint-skip -->
```js
// ./node_modules/pkg/package.json
{
  "type": "module",
  "main": "./index.js",
  "exports": {
    "./feature": {
      "import": "./feature-default.js",
      "browser": "./feature-browser.js"
    }
  }
}
```

When resolving the `"."` export, if no matching target is found, the `"main"`
will be used as the final fallback.

The conditions supported in Node.js condition matching:

* `"default"` - the generic fallback that will always match. Can be a CommonJS
   or ES module file.
* `"import"` - matched when the package is loaded via `import` or
   `import()`. Can be any module format, this field does not set the type
   interpretation.
* `"node"` - matched for any Node.js environment. Can be a CommonJS or ES
   module file.
* `"require"` - matched when the package is loaded via `require()`.

Condition matching is applied in object order from first to last within the
`"exports"` object.

Using the `"require"` condition it is possible to define a package that will
have a different exported value for CommonJS and ES modules, which can be a
hazard in that it can result in having two separate instances of the same
package in use in an application, which can cause a number of bugs.

Other conditions such as `"browser"`, `"electron"`, `"deno"`, `"react-native"`,
etc. could be defined in other runtimes or tools. Condition names must not start
with `"."` or be numbers. Further restrictions, definitions or guidance on
condition names may be provided in future.

