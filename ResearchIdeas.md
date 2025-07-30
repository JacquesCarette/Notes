A place to keep various threads that I'd like to pursue, given time. Some are questions, some are topics.

- Are terms or substitutions the 'primary' item in a type theory? The most interesting object of study are derivations, that's not the question. The point is that there are interesting substitutions that are not term-like, a la polycategories.
- Is there a good pedagogical way to explain the difference between "reason about" and "reason with" with it comes to languages and theories. There's a non-trivial 'level' difference that is frequently not talked about enough.
- What's the relation between PE (partial evaluation), slicing and supercompilation, and NbE (normalization by evaluation). Some notes on [partial evaluation](PE-Revisited.md) are looking down that road a little bit.
- NbE is related to biform theories and seems to be a particular kind of "meaning formula". Explore!
- Even more related to biform theories and meaning formulas is 'Artin Gluing'. Looks like PE and NbE are also related.
- Quantifier elimination is a particular instance of finding closed forms. There's probably a lot more "out there" that are also instances, but not recognized as such.
- What is a type? (That's a bad question, a good question is "What is a type system?") I've got tons of notes on this, really need to write them up!
- Need to remember that the duality between sums and products should yield sigma types for 'sum types' and record / Pi types (over a finite, discrete set of labels) for 'product types'. Syntactic sugar can then be added for some special cases.
- pattern-matching, especially in the 'total' case, corresponds to first doing a **partition** of the type 'space', and then a continuation is applied to each case. This is related to optics (lenses are projections, where things are first made 'cartesian'.)
- "marked contexts". In the case where a context is some fixed data-structure, it is useful to see it as (multi-) pointed, where the marks may indicate some phase transition, especially in the case when the context gets a natural order. Related to Bunched Logics.
- -1-category theory sure seems related to various kinds of logic.
- Conjecture: the category of -1-categories has 2 inhabitants iff inhabitation is decidable (i.e. likely equivalent to LEM)
- Category Theory commutative diagram proofs should really be seen as 'movies'. First, the important data is not on the nodes or edges, but inside the faces. And even that is not enough to reconstruct a proof, an order needs to be given. The act of 'focusing' that is implicit in 1-categorical proofs may also need to be made explicit, in general.
- In the case of containers, what should be seen as a 'constant'? Obviously it is a container with no positions. That doesn't mean it is necessarily trivial! It could still have (up to) infinitely many shapes.
- Typed polymorphic syntax. Such as "in the language of rings" and "in the internal language of category C". Related to programming to interfaces, obviously.
- The species Cycle has no finitely axiomatizable (in reasonable settings) equational theory. So looking at Species as related to "Free" structures (such as Bag) is too restrictive a point of view.
- Where does 'induction' come from? A lot of recursors (all for inductive types) come from the counit in the free-forgetful adjunction for an equational theory. But that does not yield induction. Is the right setting bicategorical? enriched? displayed?
- Agda's function type $A \rightarrow B$ is really (at the meta-level) $\Sigma (f : A \rightarrow B) (f \text{provably total in MLTT})$ where the function type on the right is all functions. Could rephrase in terms of provably-total functional relations to make less ambiguous.
- Further explore the idea that a language (aka syntax) is the same thing as a coordinate system. (And remember that coordinate-free linear algebra can be much nicer for semantics, and horrible for actual computations.)
- (already posted on Mastodon, but there might be more legs to it.)
language (aka syntax) is a coordinate system and vice versa.
In linear algebra, a coordinate system is a basis. Abstract linear algebra, i.e. basis free, can be much nicer than working in a specific basis. Of course, to do concrete computations, a basis is required.
In physics, coordinate systems can be crucial: doing orbital mechanics in cartesian coordinates, instead of spherical, is completely crazy.
But this argues for the need to have many (vastly different!) programming languages for different tasks.
- "Syntactic mathematics" (like closed-form expressions, but so much more). Analyze the parts of mathematics that really about the language rather than the semantics. There is quite a bit more than meets the eye. There is likely a lot of stuff that works in the initial model without saying so, for example. Of course, the amount of meta-mathematics that is syntactic dwarfs that, but that's another topic.
- Intentful types vs representation types. This is what Haskell's *newtype* should be all about, and SIP obscures (but isn't wrong!) In particular 'theories' are not adequately represented by (dependent) records.
