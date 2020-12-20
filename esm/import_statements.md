
An `import` statement can reference an ES module or a CommonJS module.
`import` statements are permitted only in ES modules, but dynamic [`import()`][]
expressions are supported in CommonJS for loading ES modules.

When importing [CommonJS modules](#esm_commonjs_namespaces), the
`module.exports` object is provided as the default export. Named exports may be
available, provided by static analysis as a convenience for better ecosystem
compatibility.

