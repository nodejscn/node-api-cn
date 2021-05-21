<!-- YAML
added: v15.0.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/38112
    description: Graduated from experimental.
-->

The `timers/promises` API provides an alternative set of timer functions
that return `Promise` objects. The API is accessible via
`require('timers/promises')`.

```mjs
import {
  setTimeout,
  setImmediate,
  setInterval,
} from 'timers/promises';
```

```cjs
const {
  setTimeout,
  setImmediate,
  setInterval,
} = require('timers/promises');
```

