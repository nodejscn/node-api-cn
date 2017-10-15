
Type: Documentation-only

`tls.parseCertString()` is a trivial parsing helper that was made public by
mistake. This function can usually be replaced with:

```js
const querystring = require('querystring');
querystring.parse(str, '\n', '=');
```

*Note*: This function is not completely equivalent to `querystring.parse()`. One
difference is that `querystring.parse()` does url decoding:

```sh
> querystring.parse('%E5%A5%BD=1', '\n', '=');
{ '好': '1' }
> tls.parseCertString('%E5%A5%BD=1');
{ '%E5%A5%BD': '1' }
```

<a id="DEP0079"></a>
