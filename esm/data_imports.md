
<!-- YAML
added: v12.10.0
-->



* `text/javascript` for ES Modules
* `application/json` for JSON
* `application/wasm` for WASM.

`data:` URLs only resolve [_Bare specifiers_][Terminology] for builtin modules
and [_Absolute specifiers_][Terminology]. Resolving

[special scheme][]. For example, attempting to load `./foo`
from `data:text/javascript,import "./foo";` will fail to resolve since there
is no concept of relative resolution for `data:` URLs. An example of a `data:`
URLs being used is:

```js
import 'data:text/javascript,console.log("hello!");';
import _ from 'data:application/json,"world!"';
```

