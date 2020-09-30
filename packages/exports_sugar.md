
> Stability: 1 - Experimental

If the `"."` export is the only export, the [`"exports"`][] field provides sugar
for this case being the direct [`"exports"`][] field value.

If the `"."` export has a fallback array or string value, then the
[`"exports"`][] field can be set to this value directly.

```json
{
  "exports": {
    ".": "./main.js"
  }
}
```

can be written:

```json
{
  "exports": "./main.js"
}
```

