
Following are some example Addons intended to help developers get started. The
examples make use of the V8 APIs. Refer to the online [V8 reference][v8-docs]
for help with the various V8 calls, and V8's [Embedder's Guide][] for an
explanation of several concepts used such as handles, scopes, function
templates, etc.

Each of these examples using the following `binding.gyp` file:

```json
{
  "targets": [
    {
      "target_name": "addon",
      "sources": [ "addon.cc" ]
    }
  ]
}
```

In cases where there is more than one `.cc` file, simply add the additional
filename to the `sources` array. For example:

```json
"sources": ["addon.cc", "myexample.cc"]
```

Once the `binding.gyp` file is ready, the example Addons can be configured and
built using `node-gyp`:

```console
$ node-gyp configure build
```


