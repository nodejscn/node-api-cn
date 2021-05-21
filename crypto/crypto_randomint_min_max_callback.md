<!-- YAML
added:
  - v14.10.0
  - v12.19.0
-->

* `min` {integer} Start of random range (inclusive). **Default:** `0`.
* `max` {integer} End of random range (exclusive).
* `callback` {Function} `function(err, n) {}`.

Return a random integer `n` such that `min <= n < max`.  This
implementation avoids [modulo bias][].

The range (`max - min`) must be less than 2<sup>48</sup>. `min` and `max` must
be [safe integers][].

If the `callback` function is not provided, the random integer is
generated synchronously.

```mjs
// Asynchronous
const {
  randomInt,
} = await import('crypto');

randomInt(3, (err, n) => {
  if (err) throw err;
  console.log(`Random number chosen from (0, 1, 2): ${n}`);
});
```

```cjs
// Asynchronous
const {
  randomInt,
} = require('crypto');

randomInt(3, (err, n) => {
  if (err) throw err;
  console.log(`Random number chosen from (0, 1, 2): ${n}`);
});
```

```mjs
// Synchronous
const {
  randomInt,
} = await import('crypto');

const n = randomInt(3);
console.log(`Random number chosen from (0, 1, 2): ${n}`);
```

```cjs
// Synchronous
const {
  randomInt,
} = require('crypto');

const n = randomInt(3);
console.log(`Random number chosen from (0, 1, 2): ${n}`);
```

```mjs
// With `min` argument
const {
  randomInt,
} = await import('crypto');

const n = randomInt(1, 7);
console.log(`The dice rolled: ${n}`);
```

```cjs
// With `min` argument
const {
  randomInt,
} = require('crypto');

const n = randomInt(1, 7);
console.log(`The dice rolled: ${n}`);
```

