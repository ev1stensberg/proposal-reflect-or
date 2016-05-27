# Reflect.logicalOR/logicalAND
ECMAScript Proposal, specs, and reference implementation for `Reflect.logicalOR/logicalAND`

Spec drafted by [@ev1stensberg](https://github.com/ev1stensberg).

This proposal is currently under no stage and is considered as a proposal, which needs to be picked up by a champion.

## Rationale
 I wanted to avoid writing foo twice(as you see in the next section) where we follow the same guidelines for both logical operators and `Reflect`. Instead of using this with prototype, I think the intent would be clearer without a constructor, since logical operators are considered somehow similar to methods such as `Math` and `Date`. Using `Reflect.logicalOR/Reflect.logicalAND` will provide a much needed static method with `Reflect` as well as it hows the clear intent of default values through the logicalOR and logicalAND. Repeating; this allows us to remove ambiguously written assignments such as `var foo = foo || bar ` and rather do `var foo = Reflect.logicalOR(foo, bar, null)`.

### Why not `var foo = foo || bar` or tenaries?
`Reflect.logicalOR()` is similar to `var foo = foo || bar`, but is different in a few critical ways:
 - When creating a object, you can pass it once, instead of being forced to either declare it twice. Note that this doesn't necessarily fix this issue, but it provides some synthetic sugar that helps us understand the use case and what we expect to happen with the object itself rather than having to read through all the code for the object that was previously written.
 - We allow logical operators to live in a cleaner ecosystem without polluting the use case, making method call static, in order to preserve its uniqueness and clear intent.
 - This makes code more readable for everyone and gives us a nice addition to existing reflection methods such as `Reflect.defineProperty()`. It also encourages interceptable JavaScript operations which again, `var foo = foo || bar` had as an intent in the first place in one way.

 Note: I haven't targeted `ReflectAND()`, the scenarios would be different but the goal is the same as stated above. 

## Naming
The reasons to stick with `logcialOR` and `logicalAND` are straightforward: it provides a relevance to both `Reflect` and the logical operators, that has a clear distinction.

I considered `Reflect.create`, but it got downvoted in ESDiscuss for bad naming and its relevance to `Object.create` and it would imply that we create a new Reflection object instead of a logicalAND/OR method on Reflect.

## Spec
You can view the spec in [markdown format](spec.md) or rendered as [HTML](http://ev1stensberg.github.io/proposal-reflect-or/).

## A little thanks

A thanks to [@ljharb](https://github.com/ljharb) for the boilerplate/promise-finally project in order for me to create this duplicate but with my proposal.
