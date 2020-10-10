
The `await` keyword may be used in the top level (outside of async functions)
within modules as per the [ECMAScript Top-Level `await` proposal][].

Assuming an `a.mjs` with

<!-- eslint-skip -->
```js
export const five = await Promise.resolve(5);
```

And a `b.mjs` with

```js
import { five } from './a.mjs';

console.log(five); // Logs `5`
```

```bash
node b.mjs # works
```

