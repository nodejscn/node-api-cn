<!-- YAML
added: v0.9.3
-->
* Returns: {string[]} An array of the names of the supported hash algorithms,
  such as `'RSA-SHA256'`.

```js
const hashes = crypto.getHashes();
console.log(hashes); // ['DSA', 'DSA-SHA', 'DSA-SHA1', ...]
```

