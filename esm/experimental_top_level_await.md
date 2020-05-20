
When the `--experimental-top-level-await` flag is provided, `await` may be used
in the top level (outside of async functions) within modules. This implements
the [ECMAScript Top-Level `await` proposal][].

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
node b.mjs # fails
node --experimental-top-level-await b.mjs # works
```

