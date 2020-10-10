
`require` always treats the files it references as CommonJS. This applies
whether `require` is used the traditional way within a CommonJS environment, or
in an ES module environment using [`module.createRequire()`][].

To include an ES module into CommonJS, use [`import()`][].

