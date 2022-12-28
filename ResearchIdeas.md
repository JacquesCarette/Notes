A place to keep various threads that I'd like to pursue, given time. Some are questions, some are topics.

- Are terms or substitutions the 'primary' item in a type theory? The most interesting object of study are derivations, that's not the question. The point is that there are interesting substitutions that are not term-like, a la polycategories.
- Is there a good pedagogical way to explain the difference between "reason about" and "reason with" with it comes to languages and theories. There's a non-trivial 'level' difference that is frequently not talked about enough.
- What's the relation between PE (partial evaluation), slicing and supercompilation, and NbE (normalization by evaluation). Some notes on [partial evaluation](PE-Revisited.md) are looking down that road a little bit.
- NbE is related to biform theories and seems to be a particular kind of "meaning formula". Explore!
- Quantifier elimination is a particular instance of finding closed forms. There's probably a lot more "out there" that are also instances, but not recognized as such.
- What is a type? (That's a bad question, a good question is "What is a type system?")
- Need to remember that the duality between sums and products should yield sigma types for 'sum types' and record / Pi types (over a finite, discrete set of labels) for 'product types'. Syntactic sugar can then be added for some special cases.
- pattern-matching, especially in the 'total' case, corresponds to first doing a **partition** of the type 'space', and then a continuation is applied to each case. This is related to optics (lenses are projections, where things are first made 'cartesian'.)
