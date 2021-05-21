
The class `Channel` represents an individual named channel within the data
pipeline. It is use to track subscribers and to publish messages when there
are subscribers present. It exists as a separate object to avoid channel
lookups at publish time, enabling very fast publish speeds and allowing
for heavy use while incurring very minimal cost. Channels are created with
[`diagnostics_channel.channel(name)`][], constructing a channel directly
with `new Channel(name)` is not supported.

