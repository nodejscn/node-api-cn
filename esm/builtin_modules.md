
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

