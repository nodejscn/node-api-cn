
The [WHATWG URL Standard][] uses a more selective and fine grained approach to
selecting encoded characters than that used by the Legacy API.

The WHATWG algorithm defines three "percent-encode sets" that describe ranges
of characters that must be percent-encoded:

* The *C0 control percent-encode set* includes code points in range U+0000 to
  U+001F (inclusive) and all code points greater than U+007E.

* The *path percent-encode set* includes the *C0 control percent-encode set*
  and code points U+0020, U+0022, U+0023, U+003C, U+003E, U+003F, U+0060,
  U+007B, and U+007D.

* The *userinfo encode set* includes the *path percent-encode set* and code
  points U+002F, U+003A, U+003B, U+003D, U+0040, U+005B, U+005C, U+005D,
  U+005E, and U+007C.

The *userinfo percent-encode set* is used exclusively for username and
passwords encoded within the URL. The *path percent-encode set* is used for the
path of most URLs. The *C0 control percent-encode set* is used for all
other cases, including URL fragments in particular, but also host and path
under certain specific conditions.

When non-ASCII characters appear within a hostname, the hostname is encoded
using the [Punycode][] algorithm. Note, however, that a hostname *may* contain
*both* Punycode encoded and percent-encoded characters. For example:

```js
const URL = require('url').URL;
const myURL = new URL('https://%CF%80.com/foo');
console.log(myURL.href);
  // Prints https://xn--1xa.com/foo
console.log(myURL.origin);
  // Prints https://π.com
```

[`Error`]: errors.html#errors_class_error
[`JSON.stringify()`]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[`Map`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
[`TypeError`]: errors.html#errors_class_typeerror
[`URLSearchParams`]: #url_class_urlsearchparams
[`array.toString()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString
[`new URL()`]: #url_constructor_new_url_input_base
[`querystring`]: querystring.html
[`require('url').format()`]: #url_url_format_url_options
[`url.domainToASCII()`]: #url_url_domaintoascii_domain
[`url.domainToUnicode()`]: #url_url_domaintounicode_domain
[`url.format()`]: #url_url_format_urlobject
[`url.href`]: #url_url_href
[`url.parse()`]: #url_url_parse_urlstring_parsequerystring_slashesdenotehost
[`url.search`]: #url_url_search
[`url.toJSON()`]: #url_url_tojson
[`url.toString()`]: #url_url_tostring
[`urlSearchParams.entries()`]: #url_urlsearchparams_entries
[`urlSearchParams@@iterator()`]: #url_urlsearchparams_iterator
[Punycode]: https://tools.ietf.org/html/rfc5891#section-4.4
[WHATWG URL Standard]: https://url.spec.whatwg.org/
[WHATWG URL]: #url_the_whatwg_url_api
[examples of parsed URLs]: https://url.spec.whatwg.org/#example-url-parsing
[percent-encoded]: #whatwg-percent-encoding
[stable sorting algorithm]: https://en.wikipedia.org/wiki/Sorting_algorithm#Stability
