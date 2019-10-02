
Policy files must use integrity checks with Subresource Integrity strings
compatible with the browser
[integrity attribute](https://www.w3.org/TR/SRI/#the-integrity-attribute)
associated with absolute URLs.

When using `require()` all resources involved in loading are checked for
integrity if a policy manifest has been specified. If a resource does not match
the integrity listed in the manifest, an error will be thrown.

An example policy file that would allow loading a file `checked.js`:

```json
{
  "resources": {
    "./app/checked.js": {
      "integrity": "sha384-SggXRQHwCG8g+DktYYzxkXRIkTiEYWBHqev0xnpCxYlqMBufKZHAHQM3/boDaI/0"
    }
  }
}
```

Each resource listed in the policy manifest can be of one the following
formats to determine its location:

1. A [relative url string][] to a resource from the manifest such as `./resource.js`, `../resource.js`, or `/resource.js`.
2. A complete url string to a resource such as `file:///resource.js`.

When loading resources the entire URL must match including search parameters
and hash fragment. `./a.js?b` will not be used when attempting to load
`./a.js` and vice versa.

To generate integrity strings, a script such as
`printf "sha384-$(cat checked.js | openssl dgst -sha384 -binary | base64)"`
can be used.

Integrity can be specified as the boolean value `true` to accept any
body for the resource which can be useful for local development. It is not
recommended in production since it would allow unexpected alteration of
resources to be considered valid.

