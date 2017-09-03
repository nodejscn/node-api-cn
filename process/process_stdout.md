
* {Stream}

`process.stdout` 属性返回连接到 `stdout` (fd `1`)的流。 
它是一个[`net.Socket`][] (它是一个[Duplex][]流)， 除非 fd `1` 指向一个文件，在这种情况下它是一个[可写][]流。

例1： 将输入流数据输出到输出流，即输出到终端。

```js
process.stdin.pipe(process.stdout);
```
例2： 要求用户输入两个数值，然后把和输出到终端。

```js
/*1:声明变量*/
var num1, num2;
/*2：向屏幕输出，提示信息，要求输入num1*/
process.stdout.write('请输入num1的值：');
/*3：监听用户的输入*/
process.stdin.on('data', function (chunk) {
    if (!num1) {
        num1 = Number(chunk);
        /*4：向屏幕输出，提示信息，要求输入num2*/
        process.stdout.write('请输入num2的值');
    } else {
        num2 = Number(chunk);
        process.stdout.write('结果是：' + (num1 + num2));
    }
});
```

注意:  重要的是`process.stdout`不同于 Node.js 的其他流,
详情可以参考[note on process I/O][] .

