<!-- YAML
added: v0.3.0
-->

* `object` {any} Any JavaScript primitive or Object.
* `options` {Object}
  * `showHidden` {boolean} If `true`, the `object`'s non-enumerable symbols and
    properties will be included in the formatted result. Defaults to `false`.
  * `depth` {number} Specifies the number of times to recurse while formatting
    the `object`. This is useful for inspecting large complicated objects.
    Defaults to `2`. To make it recurse indefinitely pass `null`.
  * `colors` {boolean} If `true`, the output will be styled with ANSI color
    codes. Defaults to `false`. Colors are customizable, see
    [Customizing `util.inspect` colors][].
  * `customInspect` {boolean} If `false`, then custom `inspect(depth, opts)`
    functions exported on the `object` being inspected will not be called.
    Defaults to `true`.
  * `showProxy` {boolean} If `true`, then objects and functions that are
    `Proxy` objects will be introspected to show their `target` and `handler`
    objects. Defaults to `false`.
  * `maxArrayLength` {number} Specifies the maximum number of array and
    `TypedArray` elements to include when formatting. Defaults to `100`. Set to
    `null` to show all array elements. Set to `0` or negative to show no array
    elements.
  * `breakLength` {number} The length at which an object's keys are split
    across multiple lines. Set to `Infinity` to format an object as a single
    line. Defaults to 60 for legacy compatibility.

The `util.inspect()` method returns a string representation of `object` that is
primarily useful for debugging. Additional `options` may be passed that alter
certain aspects of the formatted string.

The following example inspects all properties of the `util` object:

```js
const util = require('util');

console.log(util.inspect(util, { showHidden: true, depth: null }));
```

Values may supply their own custom `inspect(depth, opts)` functions, when
called these receive the current `depth` in the recursive inspection, as well as
the options object passed to `util.inspect()`.

