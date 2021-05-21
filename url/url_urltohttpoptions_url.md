<!-- YAML
added: v15.7.0
-->

* `url` {URL} The [WHATWG URL][] object to convert to an options object.
* Returns: {Object} Options object
  * `protocol` {string} Protocol to use.
  * `hostname` {string} A domain name or IP address of the server to issue the
    request to.
  * `hash` {string} The fragment portion of the URL.
  * `search` {string} The serialized query portion of the URL.
  * `pathname` {string} The path portion of the URL.
  * `path` {string} Request path. Should include query string if any.
    E.G. `'/index.html?page=12'`. An exception is thrown when the request path
    contains illegal characters. Currently, only spaces are rejected but that
    may change in the future.
  * `href` {string} The serialized URL.
  * `port` {number} Port of remote server.
  * `auth` {string} Basic authentication i.e. `'user:password'` to compute an
    Authorization header.

This utility function converts a URL object into an ordinary options object as
expected by the [`http.request()`][] and [`https.request()`][] APIs.

```js
const { urlToHttpOptions } = require('url');
const myURL = new URL('https://a:b@測試?abc#foo');

console.log(urlToHttpOptions(myUrl));
/**
{
  protocol: 'https:',
  hostname: 'xn--g6w251d',
  hash: '#foo',
  search: '?abc',
  pathname: '/',
  path: '/?abc',
  href: 'https://a:b@xn--g6w251d/?abc#foo',
  auth: 'a:b'
}
*/
```

