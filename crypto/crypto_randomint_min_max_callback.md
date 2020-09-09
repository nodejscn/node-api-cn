<!-- YAML
added: v14.10.0
-->

* `min` {integer} Start of random range (inclusive). **Default**: `0`.
* `max` {integer} End of random range (exclusive).
* `callback` {Function} `function(err, n) {}`.

Return a random integer `n` such that `min <= n < max`.  This
implementation avoids [modulo bias][].

The range (`max - min`) must be less than 2<sup>48</sup>. `min` and `max` must
be [safe integers][].

If the `callback` function is not provided, the random integer is
generated synchronously.

```js
// Asynchronous
crypto.randomInt(3, (err, n) => {
  if (err) throw err;
  console.log(`Random number chosen from (0, 1, 2): ${n}`);
});
```

```js
// Synchronous
const n = crypto.randomInt(3);
console.log(`Random number chosen from (0, 1, 2): ${n}`);
```

```js
// With `min` argument
const n = crypto.randomInt(1, 7);
console.log(`The dice rolled: ${n}`);
```

