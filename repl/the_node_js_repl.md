
Node.js itself uses the `repl` module to provide its own interactive interface
for executing JavaScript. This can be used by executing the Node.js binary
without passing any arguments (or by passing the `-i` argument):

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

