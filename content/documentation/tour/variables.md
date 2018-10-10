+++
weight = 6
title = "Variables and Mutability"
menuTitle = ""
chapter = false
hidden = false
+++

Anzen use references to make associations between a name and a value.
They're declared with the `let` keyword:

```anzen
let pokemon_level <- 1
```

Anzen is an opinionated language.
One of its opinionated choices is to prefer immutability over mutability,
meaning that by default everything is immutable.
As such, the above statement declared an *immutable reference* (a.k.a. a constant),
whose value cannot be mutated.

*Mutable references* (a.k.a. variables) must be explicitly declared,
using the *type qualifier* `@mut`:

```anzen
let level: @mut = 1
level = level + 1
```

The *semantic type* of a reference represents
the kind of values it can be associated with.
For instance, in the above example, the semantic type of the reference `level` is `Int`,
Anzen's built-in type for integer numbers.
The *contextual type* of a reference represents their capabilities (and that of their associated value),
in other words the kind of operations in which they can be used.
For instance, mutating a value is a capability that only mutable references have,
which explains why constants can't be mutated.

While the semantic type of a reference never changes,
its contextual type can,
depending on how the reference's used.
That's why it is *contextual*.
In the following example, despite `level` being declared mutable,
attempting to reassign it two statements later triggers a compilation error.
The reason is that it has been *borrowed* immutable in the second statement.
Therefore, the reference has lost its mutation capability in this particular context.

```anzen
let level: @mut = 1

let const_level &- level
level = 2
// error: cannot assign: 'level' has been moved
```

{{% notice note %}}
Notice the use of the borrow assignment `&-` at line 2,
instead of the copy assignment `=` that's been used elsewhere so far.
Assignment operators occupy a very important role in Anzen,
and will be discussed further in a later chapter.
{{% /notice %}}

Anzen uses *type inference* to automatically detect the type (semantic and contextual) of all expressions.
Some situations however require an explicit declaration,
either to go against Anzen's default typing rules (e.g. `@mut`),
or because the context does not contain enough information for Anzen to figure out the types by itself.
Such additional information are called *type annotations*:

```anzen
let list: List<Int> = []
```
