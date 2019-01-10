
默认的解释器支持直接解释 JavaScript 表达式：

<!-- eslint-skip -->
```js
> 1 + 1
2
> const m = 2
undefined
> m + 1
3
```

除非在块级作用域中或函数中，否则变量不管是隐式地声明还是使用 `const` 、 `let` 或 `var` 关键字声明，都是声明在全局作用域中。

