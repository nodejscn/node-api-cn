
All CommonJS, JSON, and C++ modules can be used with `import`.

Modules loaded this way will only be loaded once, even if their query
or fragment string differs between `import` statements.

When loaded via `import` these modules will provide a single `default` export
representing the value of `module.exports` at the time they finished evaluating.

```js
// foo.js
module.exports = { one: 1 };

// bar.js
import foo from './foo.js';
foo.one === 1; // true
```

Builtin modules will provide named exports of their public API, as well as a
default export which can be used for, among other things, modifying the named
exports. Named exports of builtin modules are updated when the corresponding
exports property is accessed, redefined, or deleted.

```js
import EventEmitter from 'events';
const e = new EventEmitter();
```

```js
import { readFile } from 'fs';
readFile('./foo.txt', (err, source) => {
  if (err) {
    console.error(err);
  } else {
    console.log(source);
  }
});
```

```js
import fs, { readFileSync } from 'fs';

fs.readFileSync = () => Buffer.from('Hello, ESM');

fs.readFileSync === readFileSync;
```

