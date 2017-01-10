
For advanced line-editors, start Node.js with the environmental variable
`NODE_NO_READLINE=1`. This will start the main and debugger REPL in canonical
terminal settings which will allow you to use with `rlwrap`.

For example, you could add this to your bashrc file:

```text
alias node="env NODE_NO_READLINE=1 rlwrap node"
```

