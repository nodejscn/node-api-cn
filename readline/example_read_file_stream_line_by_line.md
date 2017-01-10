
A common use case for `readline` is to consume input from a filesystem
[Readable][] stream one line at a time, as illustrated in the following
example:

```js
const readline = require('readline');
const fs = require('fs');

const rl = readline.createInterface({
  input: fs.createReadStream('sample.txt')
});

rl.on('line', (line) => {
  console.log(`Line from file: ${line}`);
});
```

[`process.stdin`]: process.html#process_process_stdin
[`process.stdout`]: process.html#process_process_stdout
[Writable]: stream.html
[Readable]: stream.html
[TTY]: tty.html
[`SIGTSTP`]: readline.html#readline_event_sigtstp
[`SIGCONT`]: readline.html#readline_event_sigcont
