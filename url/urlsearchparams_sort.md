<!-- YAML
added: v7.7.0
-->

Sort all existing name-value pairs in-place by their names. Sorting is done
with a [stable sorting algorithm][], so relative order between name-value pairs
with the same name is preserved.

This method can be used, in particular, to increase cache hits.

```js
const params = new URLSearchParams('query[]=abc&type=search&query[]=123');
params.sort();
console.log(params.toString());
  // Prints query%5B%5D=abc&query%5B%5D=123&type=search
```

