<!-- YAML
added: v13.6.0
-->

The REPL supports bi-directional reverse-i-search similar to [ZSH][]. It is
triggered with `<ctrl> + R` to search backwards and `<ctrl> + S` to search
forwards.

Duplicated history entires will be skipped.

Entries are accepted as soon as any button is pressed that doesn't correspond
with the reverse search. Cancelling is possible by pressing `escape` or
`<ctrl> + C`.

Changing the direction immediately searches for the next entry in the expected
direction from the current position on.

