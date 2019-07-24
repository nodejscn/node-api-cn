<!-- YAML
added: v10.6.0
-->
* `hostname` {string}

Uses the DNS protocol to resolve service records (`SRV` records) for the
`hostname`. On success, the `Promise` is resolved with an array of objects with
the following properties:

* `priority`
* `weight`
* `port`
* `name`

<!-- eslint-skip -->
```js
{
  priority: 10,
  weight: 5,
  port: 21223,
  name: 'service.example.com'
}
```

