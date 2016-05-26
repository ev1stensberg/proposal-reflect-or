# proposal-reflect-or
[WIP]Unofficial ECMAScript proposal

#Reason

Avoiding ambiguously written code and allow the OR operator to fully serve its potential. I wrote two pieces earlier about why writing code such as `var DefaultVar = DefaultVar || fallbackVar`. 

- [ESDiscuss](https://esdiscuss.org/topic/new-assignment-operators-not-bit-wise-or)
- [Medium](https://medium.com/@ev1stensberg/iteration-in-javascript-needs-a-tectonic-shift-a74b6554bbd7#.fbksisugx)


### How is this different to Default Param in ES6 / the OR operator?

 I'll try to go through most of what I was thinking and why I think they are relevant. Feel free to drop a PR or Issue if you have some feedback. I have two options in mind for this proposal.
 
***

## `Reflect.create()`

`Reflect.create(target, value, [DefaultValue])`

Creates a Reflect, which is not an object. This is used for setting an OR value with `Reflect`. 

### target
 The target object you want your values to be referenced to. You can also look at this as an argument. 
 
### value 

The second argument or object you want to refer to, if the target fails. Look at the example below for more information how this is used.

### DefaultValue

A fallsafe if the two fails, of which you can specify what should be returned if the two values fail, undefined, null or similar. This is an object, which we can turn straight into a function on the fly if we want to. 


###Example

```javascript
// without the optional fallback flag
var obj = {};
var safeValue = "Hi! This is the fallback value";
var wrapper = Reflect.create(obj, safeValue);

// with optional flag

var obj = {};
var safeValue = "Hi! This is the fallback value";
var wrapper = Reflect.create(obj, safeValue, undefined);
```

Now, if these two values fails somehow, we can avoid using tenaries/OR operators as well. If both the values fail, we will return undefined. 

This is equivalent to: 

```javascript
var obj = {};
var safeValue = "Hi! This is the fallback value";
var wrapper = obj || safeValue;

if(typeof obj === undefined && typeof safeValue === undefined) {
 wrapper == undefined
}
```

