
The default evaluator will, by default, assign the result of the most recently
evaluated expression to the special variable `_` (underscore).

```js
> [ 'a', 'b', 'c' ]
[ 'a', 'b', 'c' ]
> _.length
3
> _ += 1
4
```

Explicitly setting `_` to a value will disable this behavior.

