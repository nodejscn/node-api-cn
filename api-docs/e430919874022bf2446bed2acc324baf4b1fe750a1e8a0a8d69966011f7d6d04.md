<!-- YAML
added: v9.3.0
-->

* {string[]}

A list of the names of all modules provided by Node.js. Can be used to verify
if a module is maintained by a third party or not.

Note that `module` in this context isn't the same object that's provided
by the [module wrapper][]. To access it, require the `Module` module:

```js
const builtin = require('module').builtinModules;
```

