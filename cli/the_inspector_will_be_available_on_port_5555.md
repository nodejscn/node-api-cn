NODE_OPTIONS='--inspect=localhost:4444' node --inspect=localhost:5555
```

A flag that can be passed multiple times will be treated as if its
`NODE_OPTIONS` instances were passed first, and then its command line
instances afterwards:

```bash
NODE_OPTIONS='--require "./a.js"' node --require "./b.js"
