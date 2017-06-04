
* Returns: {string}

The `toString()` method on the `URL` object returns the serialized URL. The
value returned is equivalent to that of [`url.href`][] and [`url.toJSON()`][].

Because of the need for standard compliance, this method does not allow users
to customize the serialization process of the URL. For more flexibility,
[`require('url').format()`][] method might be of interest.

