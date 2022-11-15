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
namespace. The following information in Agda's own documentation makes that
very clear:

> The main purpose of the module system is to structure the way names are used in a program. 

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

What do we even want modules (namespaces) for?

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

Nevertheless, Agda's own documentation says:

> This is done by organising the program in an hierarchical structure of modules 
> where each module contains a number of definitions and submodules.

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

Eventually, it would be really good to support design for change. But that's
farther into the future.

### Current Features

Normally, it we would be better to have user stories here, but for expediency,
let's go with features needed/wanted. Proper requirements can be reverse
engineered from them later.

The features used right now are
1. accessing (i.e. Module.name)
2. instantiating
3. import
4. open
5. public
6. using / hiding
7. renaming
8. data and record modules built 'implicitly'

It is worthwhile expanding what the features "mean":
1. A ModNm is a (key,value) database, with keys being names, and values being
definitions.
2. A PMN is a special kind of "function" that is known to generate a ModNm.
It can be partially applied.
3. 'import' is a weird feature that stands out as it is really an interface to the
underlying file system, and is mainly used for its side-effect of making a (P)MN
visible in the current scope.
4. open is a ModNm-to-scope operation that adds all the names in a ModNm as being
directly visible in the current scope. It is side-effecting too in that sense.
However, these are made visible in a 'private' manner, in the sense that they
are not added to the external interface of the ModNm.
5. the public qualifier overrides the behaviour of open to make the names
visible publicly.
6. using and hiding are two means the change visibility of names, i.e.
  - using gives an explicit list of items now being defined,
  - hiding explicit removes an explicit list of items from an implicit list of "all" names
7. renaming provides a way to locally change the names of definitions.

### Wanted Features

1. sharing
2. module interfaces (i.e. module types)
3. module interface combinators

## Design

(This is written in a rush, to get feedback, and should not be understood as
being more than a placeholder. In particular, the proposal seems like a bit of
a leap given the rest of the write-up.)

### Background

**Important remark**: records types, telescopes, theories and contexts are, in dependent
type theory "the same thing". There are versions of all of these that can be
understood as associating names to types (and more). Some even include conservative extensions,
aka definitions, even though they are "at the type level".

### Proposal, Part 1

Merge (at least) records (as values) and modules (as containers of implementations).
Preserve a 'marker' that would recall the intent of use, so that some features can be
enabled/disabled for each, if so desired. 

For example, it might make sense to not allow 'open' in a record declaration,
as that would mean that creating record values might have side effects. But then
again, one can essentially hack things up now by using anonymous modules (both
surrounding a declaration and local ones). So maybe this isn't even a big deal.

Pros:
- significant simplification of code base
- no need to 'generate' modules for records
- Module types
- First class modules
- Generative records
- Records can now have private and abstract fields
- No need to define dummy records to get to use selector syntax

Cons:
- very large surgery
- would allow dependent record fields

### Proposal, Part 2

Introduce 'Let' in the Agda AST. Reason: preserve sharing.

Change module instantiation to use 'Let' instead of using substitution.
Furthermore, do not put independent lambdas on each 'name' in a module,
but leave them be on the 'outside'. As parametrized modules are
already transparent, these parameters would continue to be so (i.e. in
some ways behave as if they were all implicit, whether they actually are or not.)

### Proposal, Part 3

Introduce signature combinators. Different combinators would produce different
results (some would give the data of a pullback, for example), so that some
syntax would be needed to "extract" concrete signature objects. This is needed
to enable various combinations and diagram-level combinators.

----

## Misc Notes

These will need to be moved up into the main text when the proper place
appears.

Below, ModNm is used for modules / namespaces, for brevity. ParModNm, and
even PMN, for "parametrized modules / namespaces".

### Parametrized modules / namespaces

- parameters are not ModNm themselves! They are values from a type.
So here too Agda's modules are quite second-class.
- PMN are basically functions which are return a MonNm, i.e. generators.
- However PMN are "transparent" in that the names that are eventually bound
are visible even if a ModNm is not even applied. This is useful but weird.

### Likely Needed

Any next-gen version of 'module' is most likely to need a *Let* addition to the
internal AST. This is the sanest way to maintain sharing.

### Problems

Syntax and pattern declarations have a weird status as definitions in a module.
