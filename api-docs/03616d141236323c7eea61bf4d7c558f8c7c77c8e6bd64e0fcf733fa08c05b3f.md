<!-- YAML
added: v0.9.3
-->
* Returns: {string[]} An array with the names of the supported cipher
  algorithms.

```js
const ciphers = crypto.getCiphers();
console.log(ciphers); // ['aes-128-cbc', 'aes-128-ccm', ...]
```

