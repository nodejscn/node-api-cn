<!-- YAML
added: v8.0.0
-->

Immediately close the session. All pending message callbacks will be called
with an error. [`session.connect()`] will need to be called to be able to send
messages again. Reconnected session will lose all inspector state, such as
enabled agents or configured breakpoints.

