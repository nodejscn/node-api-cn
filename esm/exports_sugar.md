
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

