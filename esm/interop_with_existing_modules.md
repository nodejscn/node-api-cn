
All CommonJS, JSON, and C++ modules can be used with `import`.

Modules loaded this way will only be loaded once, even if their query
or fragment string differs between `import` statements.

When loaded via `import` these modules will provide a single `default` export
representing the value of `module.exports` at the time they finished evaluating.

```js
import fs from 'fs';
fs.readFile('./foo.txt', (err, body) => {
  if (err) {
    console.error(err);
  } else {
    console.log(body);
  }
});
```

