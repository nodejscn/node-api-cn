
> Stability: 2 - Stable

The `readline` module provides an interface for reading data from a [Readable][]
stream (such as [`process.stdin`]) one line at a time. It can be accessed using:

```js
const readline = require('readline');
```

The following simple example illustrates the basic use of the `readline` module.

```js
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('What do you think of Node.js? ', (answer) => {
  // TODO: Log the answer in a database
  console.log(`Thank you for your valuable feedback: ${answer}`);

  rl.close();
});
```

*Note* Once this code is invoked, the Node.js application will not
terminate until the `readline.Interface` is closed because the interface
waits for data to be received on the `input` stream.

