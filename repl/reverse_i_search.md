<!-- YAML
added: v13.6.0
-->

The REPL supports bi-directional reverse-i-search similar to [ZSH][]. It is
triggered with **Ctrl+R** to search backward and **Ctrl+S** to search
forwards.

Duplicated history entires will be skipped.

Entries are accepted as soon as any button is pressed that doesn't correspond
with the reverse search. Cancelling is possible by pressing **Esc** or
**Ctrl+C**.

Changing the direction immediately searches for the next entry in the expected
direction from the current position on.

