
The default evaluator supports direct evaluation of JavaScript expressions:

```js
> 1 + 1
2
> var m = 2
undefined
> m + 1
3
```

Unless otherwise scoped within blocks (e.g. `{ ... }`) or functions, variables
declared either implicitly or using the `var` keyword are declared at the
`global` scope.

