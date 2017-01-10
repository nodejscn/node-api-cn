<!-- YAML
added: v0.9.12
-->

Uses the DNS protocol to resolve regular expression based records (`NAPTR`
records) for the `hostname`. The `callback` function has arguments
`(err, addresses)`.  The `addresses` argument passed to the `callback` function
will contain an array of objects with the following properties:

* `flags`
* `service`
* `regexp`
* `replacement`
* `order`
* `preference`

For example:

```js
{
  flags: 's',
  service: 'SIP+D2U',
  regexp: '',
  replacement: '_sip._udp.example.com',
  order: 30,
  preference: 100
}
```

