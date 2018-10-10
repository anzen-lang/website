---
title: "Anzen"
---

# Anzen

Anzen is a general-purpose programming language
that aims at bridging the gap between modern programming and software verification.

The goal of the Anzen is to offer a modern approach to programming,
through the support of several paradigms,
while also embedding a comprehensive built-in support
for static (a.k.a. compile-time) and dynamic (a.k.a. run-time) checks.
The language comes with a powerful program checker that uses the code itself as a model
to detect errors and design test scenarios.


### Why Anzen?

Anzen aims at being as accessible as popular modern scripting languages:

```anzen
let attributes <- [ "simple", "concise", "safe" ]
for let attr in attributes {
  print("Anzen is " + attr)
}
```

Anzen does not need overly verbose type annotations,
yet it is equipped with a powerful built-in support for complex static constraint verification,
such as:

**Type safety**
Code should clearly express the programmer's intention,
and should always behave accordingly,
leaving no place for undefined behavior.
This is why Anzen places a strong emphasis on types,
making sure variables always hold values of the type they are supposed to.

```anzen
var x <- 42
// error: cannot assign a r-value of type 'String' to a l-value of type 'Int'
x <- "foo"
```

**Memory safety**
Type safety is often insufficient to guarantee the correctness of a code,
as one as also to make sure memory is properly initialized, accessed and freed.
Anzen features a powerful memory model that can make guarantees on safe memory operations.

```anzen
let fruits: @mut <- [ "apple", "orange", "peach" ]
for fruit in fruits {
  // error: cannot call mutating method 'remove' on reference borrowed immutable
  fruits.remove(at <- fruits.index(of &- fruit))
}
```

**Semantic conformance**
While Java-like interfaces allows for syntactical conformance to be expressed,
Anzen also supports the definition of semantic interfaces
to describe semantic constraints.

```anzen
interface OrderedCollection refines Collection
  where
    Element is Comparable
  ensures
    forall x: Self.Index, forall y: Self.Index,
      (x < y) implies (self[x] <= self[y])
{
  get min: Element { return self[self.first_index] }
  get max: Element { return self[self.last_index] }
}
```

Check out the section about Safety for more information about what Anzen can offer.
