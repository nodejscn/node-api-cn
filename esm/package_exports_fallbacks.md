
For possible new specifier support in future, array fallbacks are
supported for all invalid specifiers:

<!-- eslint-skip -->
```js
{
  "exports": {
    "./submodule": ["not:valid", "./submodule.js"]
  }
}
```

Since `"not:valid"` is not a valid specifier, `"./submodule.js"` is used
instead as the fallback, as if it were the only target.

