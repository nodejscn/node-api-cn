
Used to prevent an abort if a string decoder was set on the Socket.

```js
const Socket = require('net').Socket;
const instance = new Socket();

instance.setEncoding('utf8');
```

<a id="ERR_STRING_TOO_LARGE"></a>
