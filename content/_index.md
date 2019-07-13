---
title: "Anzen"
---

# Anzen

Anzen is a multi-paradigm programming language that aims to make assignments easier to understand and manipulate.
Its goal is to offer a modern approach to programming while building on a sound and unambiguous semantics,
in particular with respect to the treatment of memory.

## Why Anzen?

Anzen's most distinguishing characteristic is that it features three different assignment operators.
Unlike most other contemporary programming languages,
these operators independent of their operands' types and provide the following strategies.
This means that there are no differences between primitive, value or reference types.

- An aliasing operator `&-` assigns an alias on the object on its right to the reference on its left.
  Its semantics is the closest to what is generally understood as an assignment in languages that abstract over pointers (e.g. Python or Java).
- A copy operator `:=` assigns a deep copy of the object's value on its right to the reference on its left.
  If the left operand was already bound to an object, the copy operator mutates its value rather than reassigning the reference to a different one.
- A move operator `<-` moves the object on its right to the reference on its left.
  If the right operand was a reference, the move operator removes its binding, effectively leaving it unusable until it is reassigned.

Here is an example:

```anzen
let x: @mut <- "Hello, World!"
print(x)
// Prints "Hello, World!"

let y: @mut &- x
print(y)
// Prints "Hello, World!"

x := "Hi, Universe!"
print(y)
// Prints "Hi, Universe!"
```

On the top of these operators, Anzen implements with a plethora of modern programming concepts,
gifting it with clear and concise syntax.

The other strength of Anzen is the emphasis it puts on safety.

**Type safety**:
Code should clearly express the programmer's intention,
and should always behave accordingly,
leaving no place for undefined behavior.
This is why Anzen places a strong emphasis on types,
making sure variables always hold values of the type they are supposed to.

```anzen
var x <- 42
x <- "foo"
// error: cannot assign a r-value of type 'String' to a l-value of type 'Int'
```

**Memory safety**:
Type safety is often insufficient to guarantee the correctness of a code,
as one as also to make sure memory is properly initialized, accessed and freed.
Anzen features a powerful memory model that can make guarantees on safe memory operations.

```anzen
let fruits: @mut <- [ "apple", "orange", "peach" ]
for fruit in fruits {
  fruits.remove(at <- fruits.index(of &- fruit))
  // error: cannot call mutating method 'remove' on reference borrowed immutable
}
```

**Semantic conformance (future development)**:
While Java-like interfaces allows for syntactical conformance to be expressed,
future developments include support for semantic interfaces to describe semantic constraints.

```anzen
interface OrderedCollection refines Collection
  where
    Element is Comparable
  ensures
    forall x: Self.Index, forall y: Self.Index,
      (x < y) implies (self[x] <= self[y])
{
  fun min() -> Element { return self[self.first_index] }
  fun max() -> Element { return self[self.last_index] }
}
```

Check out the section about Safety for more information about what Anzen can offer.

## Try Anzen

A compiler and interpreter for Anzen are distributed as an open-source software,
written in [Swift](https://developer.apple.com/swift/),
and available on Github: https://github.com/anzen-lang/anzen.
Checkout the instructions to install Anzen on your machine.
