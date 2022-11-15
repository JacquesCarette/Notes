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

The use of names is of course crucial for one purpose:
**being able to access them externally**. The biggest difference between
modules (and namespaces) and lambda-term (and contexts) is the ability
to ``zoom in'' directly to one piece, without the need to use some
unary codes. (Humans are not Borg.) 

### What is a Module System?

The question "what is a module" is not particularly interesting, even when augmented
to deal with parametrized modules. This is because having a single module around
doesn't really help, the real desire is to have many modules. So we need to
worry about how modules interact, refer to each other, and so on.

There doesn't seem to be as simple an answer here.

## Requirements Analysis

What do even want modules (namespaces) for?

At the simplest level, we know that libraries grow to be quite large, as there simply
are many different concepts to express. At the absolute minimum, there needs to be
tools to help organize lots of code.

Luckily, code doesn't normally consist of random artifacts. It expresses various
kinds of (organized) knowledge. Now, it should be clear that a purely hierarchical
organization is **completely hopeless**. There are concepts that will always want
to 'sit' in multiple parts of some purely tree-like hierarchy. Going to a directed
acyclic graph helps a tiny bit, but doesn't solve the fundamental issue that there
are non-trivial isomorphisms between bits of knowledge that seem to belong in
different places, no matter how one slices things up. [Some references for this would
be nice, later.]

This doesn't mean we have to abandon hierarchies! It merely means that the
hierarchy should not be taken too seriously, and that other means to
relate information must be supported too. Whether to do via allowing
duplication and using post-facto isomorphisms, or going with generative 
morphisms, or both, is an open design question.

Nevertheless, one question to look at is "how do we come up with 'good'
modules?"

### Design for Change

Parnas in his 1973 paper on information hiding (insert link here) provides
a time-tested answer: if we know that certain things are likely to change
in the future, then that aspect of the change should be **hidden** behind
an abstraction barrier. One good process to follow to identify good
modules is to divide the information contained in a module to that 
which ought to be secret (often consists of implementation details, but
there are others things one may hide as well) and those that can be
exposed to the world, via an interface.

It's important to remember that Parnas never insisted that 'hiding' be
something that must be done *in* a language, never mind being enforced
by the language itself. Human-convention interfaces are perfectly
acceptable. Furthermore, and wildly misunderstood as well, there is no
requirement whatsoever that modules persist *at run time*. That the compiler
may inline everything is perfectly allowable. Interestingly, Parnas doesn't
believe that modules necessarily need to exist in the code either - as long
as they exist in the design and the mapping from the design to the implementation
is clear, it's ok to write "messy" implementations. A more modern way to
think of this is from the point of view of generative programming (whether 
C++ templates, metaocaml, template haskell, or various hacked up means
doesn't really matter.)
