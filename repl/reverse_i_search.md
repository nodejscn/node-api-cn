<!-- YAML
added:
 - v13.6.0
 - v12.17.0
-->

The REPL supports bi-directional reverse-i-search similar to [ZSH][]. It is
triggered with <kbd>Ctrl</kbd>+<kbd>R</kbd> to search backward and
<kbd>Ctrl</kbd>+<kbd>S</kbd> to search
forwards.

Duplicated history entries will be skipped.

Entries are accepted as soon as any key is pressed that doesn't correspond
with the reverse search. Cancelling is possible by pressing <kbd>Esc</kbd> or
<kbd>Ctrl</kbd>+<kbd>C</kbd>.

Changing the direction immediately searches for the next entry in the expected
direction from the current position on.

