<!-- YAML
added: v10.12.0
deprecated: v12.2.0
-->

* `filename` {string} Filename to be used to construct the relative require
  function.
* Returns: {require} Require function

> Stability: 0 - Deprecated: Please use [`createRequire()`][] instead.

```js
const { createRequireFromPath } = require('module');
const requireUtil = createRequireFromPath('../src/utils/');

// Require `../src/utils/some-tool`
requireUtil('./some-tool');
```














