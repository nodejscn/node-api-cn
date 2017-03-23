
<!--type=misc-->

Sometimes, the domain in use is not the one that ought to be used for a
specific event emitter.  Or, the event emitter could have been created
in the context of one domain, but ought to instead be bound to some
other domain.

For example, there could be one domain in use for an HTTP server, but
perhaps we would like to have a separate domain to use for each request.

That is possible via explicit binding.

For example:

```js
// create a top-level domain for the server
const domain = require('domain');
const http = require('http');
const serverDomain = domain.create();

serverDomain.run(() => {
  // server is created in the scope of serverDomain
  http.createServer((req, res) => {
    // req and res are also created in the scope of serverDomain
    // however, we'd prefer to have a separate domain for each request.
    // create it first thing, and add req and res to it.
    const reqd = domain.create();
    reqd.add(req);
    reqd.add(res);
    reqd.on('error', (er) => {
      console.error('Error', er, req.url);
      try {
        res.writeHead(500);
        res.end('Error occurred, sorry.');
      } catch (er2) {
        console.error('Error sending 500', er2, req.url);
      }
    });
  }).listen(1337);
});
```

