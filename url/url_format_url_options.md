<!-- YAML
added: v7.6.0
-->

* `URL` {URL} A [WHATWG URL][] object
* `options` {Object}
  * `auth` {boolean} `true` if the serialized URL string should include the
    username and password, `false` otherwise. Defaults to `true`.
  * `fragment` {boolean} `true` if the serialized URL string should include the
    fragment, `false` otherwise. Defaults to `true`.
  * `search` {boolean} `true` if the serialized URL string should include the
    search query, `false` otherwise. Defaults to `true`.
  * `unicode` {boolean} `true` if Unicode characters appearing in the host
    component of the URL string should be encoded directly as opposed to being
    Punycode encoded. Defaults to `false`.

Returns a customizable serialization of a URL String representation of a
[WHATWG URL][] object.

The URL object has both a `toString()` method and `href` property that return
string serializations of the URL. These are not, however, customizable in
any way. The `url.format(URL[, options])` method allows for basic customization
of the output.

For example:

```js
const myURL = new URL('https://a:b@你好你好?abc#foo');

console.log(myURL.href);
  // Prints https://a:b@xn--6qqa088eba/?abc#foo

console.log(myURL.toString());
  // Prints https://a:b@xn--6qqa088eba/?abc#foo

console.log(url.format(myURL, {fragment: false, unicode: true, auth: false}));
  // Prints 'https://你好你好?abc'
```

