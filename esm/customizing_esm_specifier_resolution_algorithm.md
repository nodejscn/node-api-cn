
The current specifier resolution does not support all default behavior of
the CommonJS loader. One of the behavior differences is automatic resolution
of file extensions and the ability to import directories that have an index
file.

The `--es-module-specifier-resolution=[mode]` flag can be used to customize
the extension resolution algorithm. The default mode is `explicit`, which
requires the full path to a module be provided to the loader. To enable the
automatic extension resolution and importing from directories that include an
index file use the `node` mode.

```bash
$ node --experimental-modules index.mjs
success!
$ node --experimental-modules index #Failure!
Error: Cannot find module
$ node --experimental-modules --es-module-specifier-resolution=node index
success!
```

















