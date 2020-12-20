
Modules are loaded multiple times if the `import` specifier used to resolve
them has a different query or fragment.

```js
import './foo.mjs?query=1'; // loads ./foo.mjs with query of "?query=1"
import './foo.mjs?query=2'; // loads ./foo.mjs with query of "?query=2"
```

The volume root may be referenced via `/`, `//` or `file:///`. Given the
differences between [URL][] and path resolution (such as percent encoding
details), it is recommended to use [url.pathToFileURL][] when importing a path.

