
The default evaluator will, by default, assign the result of the most recently
evaluated expression to the special variable `_` (underscore).

默认的解释器会把下划线`_`解释为最近一次执行的表达式。

```js
> [ 'a', 'b', 'c' ]
[ 'a', 'b', 'c' ]
> _.length
3
> _ += 1
4
```

Explicitly setting `_` to a value will disable this behavior.

显式设置下划线`_`为某个值 会禁用上述行为。
