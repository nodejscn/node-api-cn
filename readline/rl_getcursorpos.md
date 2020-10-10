<!-- YAML
added:
 - v13.5.0
 - v12.16.0
-->

* Returns: {Object}
  * `rows` {number} the row of the prompt the cursor currently lands on
  * `cols` {number} the screen column the cursor currently lands on

Returns the real position of the cursor in relation to the input
prompt + string. Long input (wrapping) strings, as well as multiple
line prompts are included in the calculations.

