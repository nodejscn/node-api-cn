<!-- YAML
added: v0.1.27
-->

Uses the DNS protocol to resolve service records (`SRV` records) for the
`hostname`. The `addresses` argument passed to the `callback` function will
be an array of objects with the following properties:

* `priority`
* `weight`
* `port`
* `name`

```js
{
  priority: 10,
  weight: 5,
  port: 21223,
  name: 'service.example.com'
}
```

