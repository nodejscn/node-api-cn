
> Stability: 1 - Experimental

If found, Source Map data is appended to the top-level key `source-map-cache`
on the JSON coverage object.

`source-map-cache` is an object with keys representing the files source maps
were extracted from, and the values include the raw source-map URL
(in the key `url`) and the parsed Source Map V3 information (in the key `data`).

```json
{
  "result": [
    {
      "scriptId": "68",
      "url": "file:///absolute/path/to/source.js",
      "functions": []
    }
  ],
  "source-map-cache": {
    "file:///absolute/path/to/source.js": {
      "url": "./path-to-map.json",
      "data": {
        "version": 3,
        "sources": [
          "file:///absolute/path/to/original.js"
        ],
        "names": [
          "Foo",
          "console",
          "info"
        ],
        "mappings": "MAAMA,IACJC,YAAaC",
        "sourceRoot": "./"
      }
    }
  }
}
```

