# proposal-reflect-or
[WIP]Unofficial ECMAScript proposal

#Reason

Avoiding ambiguously written code and allow the OR operator to fully serve its potential. I wrote two pieces earlier about why writing code such as `var DefaultVar = DefaultVar || fallbackVar`. 

- [ESDiscuss](https://esdiscuss.org/topic/new-assignment-operators-not-bit-wise-or)
- [Medium](https://medium.com/@ev1stensberg/iteration-in-javascript-needs-a-tectonic-shift-a74b6554bbd7#.fbksisugx)


### How is this different to Default Param in ES6 / the OR operator?

There's some breaking changes. One of which, we can steal the from proxies. I'll try to go through most of them and why I think they are relevant. Feel free to drop a PR or Issue if you have some feedback.
***
## `Reflect.apply()`

Giving a shot at trying to keep this somewhat similar to our existing opportunities. Note that we assume our `DefaultVar` and `fallbackVar` has already been set, we define our method like this. This allows us to set an new object that acts like a container while preserving the context of our two values(See next section). It will return undefined if otherwise. A crazy idea, would be to get undefined to be swapped out with a promise in order to make sure we get either one of these values. 

`Reflect.apply(DefaultVar, undefined, fallbackVar); `

***
## `Reflect.construct()` 

Similar to what we had above, alltough, this acts like a `new Something` rather than calling the context it was set in. The difference from this and `Reflect.apply()` is that we can make this as a container object rather than directly invoking. 
