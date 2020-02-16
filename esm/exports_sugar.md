
If the `"."` export is the only export, the `"exports"` field provides sugar
for this case being the direct `"exports"` field value.

If the `"."` export has a fallback array or string value, then the `"exports"`
field can be set to this value directly.

<!-- eslint-skip -->
```js
{
  "exports": {
    ".": "./main.js"
  }
}
```

can be written:

<!-- eslint-skip -->
```js
{
  "exports": "./main.js"
}
```

When using [Conditional Exports][], the rule is that all keys in the object
mapping must not start with a `"."` otherwise they would be indistinguishable
from exports subpaths.

<!-- eslint-skip -->
```js
{
  "exports": {
    ".": {
      "import": "./main.js",
      "require": "./main.cjs"
    }
  }
}
```

can be written:

<!-- eslint-skip -->
```js
{
  "exports": {
    "import": "./main.js",
    "require": "./main.cjs"
  }
}
```

If writing any exports value that mixes up these two forms, an error will be
thrown:

<!-- eslint-skip -->
```js
{
  // Throws on resolution!
  "exports": {
    "./feature": "./lib/feature.js",
    "import": "./main.js",
    "require": "./main.cjs"
  }
}
```

