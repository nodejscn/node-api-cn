<!--
added: v8.0.0
-->

[`Serializer`][]的子类，用来将`TypedArray`(尤其是[`Buffer`][])和`Dataview`序列化成一个宿主对象，并且对于它们底层的`ArrayBuffer`，只有被它们实际指向的部分会被存储起来。
