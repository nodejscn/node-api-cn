
Type: Documentation-only

Importing assert directly is not recommended as the exposed functions will use
loose equality checks. Use `require('assert').strict` instead. The API is the
same as the legacy assert but it will always use strict equality checks.

<a id="DEP0090"></a>
