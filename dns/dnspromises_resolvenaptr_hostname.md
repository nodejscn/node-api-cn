<!-- YAML
added: v10.6.0
-->

* `hostname` {string}

Uses the DNS protocol to resolve regular expression based records (`NAPTR`
records) for the `hostname`. On success, the `Promise` is resolved with an array
of objects with the following properties:

* `flags`
* `service`
* `regexp`
* `replacement`
* `order`
* `preference`

<!-- eslint-skip -->
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

