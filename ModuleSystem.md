# What is a Module (System)?

This is a set of notes trying to puzzle out what a module system could be for Agda.

## Preliminary "What is"

Before trying to define the full ideas, it is quite useful to first understand what
might be simpler cases.

### What is a Module?

That is quite straightforward:

> A module is an implementation of an interface.

A slightly expanded definition would read

> A module is an implementation in a language L that satisfies an interface written
> in a language L'.

There are 3 open parameters (on purpose) in that definition:
1. The language L (and its well-formedness rules, possibly typing rules, etc)
2. The language L' (ditto)
3. The meaning of 'satisfies'.

In particular, L' could be "English", L could be "pseudo-code" and satisfied could be
entirely informal. At the opposite end, L and L' could be part of the same language,
and satifies might be defined by the rules of that language.

At this point, there is an obvious remark to make: the things called modules in
Agda don't satisfy any interface! So it is worthwhile to make a detour to
describe something related to modules that will let us understand what is currently
implemented.

### What is a Namespace?

So if we really weaken "satisfies an interface" to "exports a bunch of names"
(and is well-formed). We didn't actually talk about names yet... so it's worth
first expanding that out first.

#### Names?

There is an implicit assumption that an 'implementation' is actually an association
of a bunch of (potentitally typed) terms to names. This means that a 'signature' must also
match that. Unsurprisingly, that ends up looking very much like records and
record signatures.

Well, 'term' is not quite right, is it? That doesn't quite allow `data` and `record`
declarations. What's really meant here is some kind of "definition". So rather than
'term', let's use the more general Definition for that syntactic class.

#### Namespace

So we have (using Haskell's `Data.These`):

> A Namespace is an association of names to `These Type Definition`.

Just to be clear:
- `This Type` corresponds to a postulate
- `That Definition` corresponds to a bare implementation
- `These Type Definition` corresponds to a properly typed implementation

(In Agda, using `(Type, Maybe Definition)` to disallow bare implementations is probably
better?)

#### Agda

It should be clear that Agda's (unparametrized) `module` corresponds to a
namespace.
