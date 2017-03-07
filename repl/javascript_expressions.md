
The default evaluator supports direct evaluation of JavaScript expressions:
默认的解释器支持直接解释JavaScript表达式：

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
除非在块级作用域中（如`{...}`）或函数中，变量不管是用隐式声明还是使用`var`关键字声明，都是在`全局`中声明。
