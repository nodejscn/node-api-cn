
<!-- YAML
added: v14.13.1
-->

`node:` URLs are supported as an alternative means to load Node.js builtin
modules. This URL scheme allows for builtin modules to be referenced by valid
absolute URL strings.

```js
import fs from 'node:fs/promises';
```

