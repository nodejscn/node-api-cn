<!-- YAML
added: v10.12.0
-->

* `filename` {string} Filename to be used to construct the relative require
  function.
* Returns: {[`require`][]} Require function

```js
const { createRequireFromPath } = require('module');
const requireUtil = createRequireFromPath('../src/utils');

// require `../src/utils/some-tool`
requireUtil('./some-tool');
```












