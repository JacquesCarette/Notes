# Evaluation Modulo Theories or Partial Evaluation Revisited

The 'simple' way to see PE is that it uses a single bit of information (static or dynamic) along with an operational semantics (defined by an interpreter) to define what PE does. Multiple applications then 'does magic'.

The offline version of PE does a preliminary abstract interpretation that propagates this static/dynamic classification. Then a partial evaluator takes the marked program and reduces everything that it can. An online version computes static/dynamic as it goes, and is much more precise because of it. Still, this doesn't work so well.

The first thing that is done is various program transformations that preserve contextual equivalence. PE is a program transformation, after all, so this isn't so far fetched. And the PE equations are all observational in nature too, i.e. viewing programs as input-output machines. Though, of course, for side-effecting languages, these must be preserved too.

So the interpreter really is a convenience, especially when it is written in the same programming language as the programs we're evaluating: it gives an executable 'reference semantics'. But it can only capture what's visible through reductions. The validity of program transformations (like translation to CPS) must really be proven externally.

The other thing that this doesn't handle so well is *partially static data*. For example, we know that terms over the integers extended with variables (i.e. dealing with open terms over (Z, 0, 1, add, mul) ) are polynomials, which have a wealth of normal forms. Most beautifully, this can all be done via arithmetic rather than rewrites, resulting in significantly faster work. This generalizes - that's what FREX is all about.

Other uses of PE go further: MaplePE changes the language (to say more, carry more invariants, etc). The work on FFT in metaocaml adds some extra abstract interpretation to make things better. There's other work that uses eta-expansion.

An obvious question is: does this all have something in common? The answer is yes: rather than viewing partial evaluation as getting rid of a layer of interpretation, we can also see it as a walk in the space of programs, modulo its equational theory. It is really important that the equational theory used be extended to one that deals with open terms (i.e. terms in context): most program fragments are not closed. We can then see things as reductions that look like

context |- term => context' |- term'

where the context is not limited to just variable declarations but can also contain relational information, i.e. anything valid from the equational theory. (That should probably be generalized further.) In a way, this is what moves us from PE to supercompilation! The point is that various parts of a program can *reduce*, or at least be rewritten to be "simpler", given the right properties hold of the current term in focus.

The whole point being that this gives a uniform explanation to a lot of ad hoc seeming features one encounters in the literature.
