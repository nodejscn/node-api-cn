
When a policy check fails, Node.js by default will throw an error.
It is possible to change the error behavior to one of a few possibilities
by defining an "onerror" field in a policy manifest. The following values are
available to change the behavior:

* `"exit"` - will exit the process immediately.
    No cleanup code will be allowed to run.
* `"log"` - will log the error at the site of the failure.
* `"throw"` (default) - will throw a JS error at the site of the failure.

```json
{
  "onerror": "log",
  "resources": {
    "./app/checked.js": {
      "integrity": "sha384-SggXRQHwCG8g+DktYYzxkXRIkTiEYWBHqev0xnpCxYlqMBufKZHAHQM3/boDaI/0"
    }
  }
}
```

