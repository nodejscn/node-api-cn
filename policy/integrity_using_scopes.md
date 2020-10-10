
Setting an integrity to `true` on a scope will set the integrity for any
resource not found in the manifest to `true`.

Setting an integrity to `null` on a scope will set the integrity for any
resource not found in the manifest to fail matching.

Not including an integrity is the same as setting the integrity to `null`.

`"cascade"` for integrity checks will be ignored if `"integrity"` is explicitly
set.

The following example allows loading any file:

```json
{
  "scopes": {
    "file:": {
      "integrity": true
    }
  }
}
```

