Node.js自身也使用`repl`模块，用来提供执行自身JavaScript代码的交互界面。不带任何参
数执行Node.js二进制代码（或者使用`-i`参数）


```js
$ node
> a = [1, 2, 3];
[ 1, 2, 3 ]
> a.forEach((v) => {
...   console.log(v);
...   });
1
2
3
```

