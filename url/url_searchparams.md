
* {URLSearchParams}

获取表示 URL 查询参数的 [`URLSearchParams`] 对象。
This property is read-only but the `URLSearchParams` object it provides
can be used to mutate the URL instance; to replace the entirety of query
parameters of the URL, use the [`url.search`][] setter. See
[`URLSearchParams`][] documentation for details.

Use care when using `.searchParams` to modify the `URL` because,
per the WHATWG specification, the `URLSearchParams` object uses
different rules to determine which characters to percent-encode. For
instance, the `URL` object will not percent encode the ASCII tilde (`~`)
character, while `URLSearchParams` will always encode it:

```js
const myUrl = new URL('https://example.org/abc?foo=~bar');

console.log(myUrl.search);  // prints ?foo=~bar

// Modify the URL via searchParams...
myUrl.searchParams.sort();

console.log(myUrl.search);  // prints ?foo=%7Ebar
```

