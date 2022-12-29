# Generic Programming Revisited

There are multiple notions of generic programming:
- polytypic, or datatype-generic programming
- parametric polymorphism
- "theory" polymorphism, or interface polymorphism, which are my names for the original Musser-Stepanov vision

And a number of methods that really are quite like generic programming:
- others kinds of polymorphism?
- various kinds of "a la Carte" approaches

At the end of the day, one can say that the in various languages, "generic programming" is 
the label that's used for the kinds of polymorphism that the language doesn't have, or at least
doesn't support very well.

In related work, there is:
- Jeremy Gibbon's [Datatype−Generic Programming](https://www.cs.ox.ac.uk/publications/publication1397-abstract.html) chapter, 
- Garcia et al.'s [An extended comparative study of language support for generic programming](https://www.cambridge.org/core/journals/journal-of-functional-programming/article/an-extended-comparative-study-of-language-support-for-generic-programming/C97D5964ECC2E651EEF9A70BC50600A6) 
- Siek-Lumsdaine[A language for generic programming in the large](https://www.sciencedirect.com/science/article/pii/S0167642308001123)
- Chetioui, Jaarvi, Haveraaen's [Revisiting Language Support for Generic Programming: When Genericity Is a Core Design Goal](https://arxiv.org/abs/2211.01678) (and its list of references)

ToDo:
- give full, good examples of each kind
- find more papers (i.e. after the obvious survey papers) that really are about new kinds of polymorphism
- redo the examples as polymorphism over an initial segment of a context/telescope.

Polytypic is trickier because it involves a syntax/semantics loop. But once that's out of the way,
the link to staging and generative programming becomes clear, so that the C++ approach to this
does not seem ad hoc at all anymore.

At the end of the day, it's all various kinds of "programming to an interface". Why it all looks so
different, other than the wildly different syntaxes of different languages, is that the restrictions
on the interfaces or, at the other extreme, the permissiveness of the language of interfaces, makes
what one can effectively say quite different.
