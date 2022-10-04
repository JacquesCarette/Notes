This is inspired by James Koppel's [blog post](https://www.pathsensitive.com/2022/09/bet-you-cant-solve-these-9-dependency.html) on "software dependence". Interested readers should also read his paper (co-authored with Daniel Jackson) [Demystifying Dependence](https://www.jameskoppel.com/files/papers/demystifying_dependence.pdf).

The purpose is to see if we can model, mathematically, what that paper says. First, let's get some red herrings out of the way.

A naive mathematical approach would invoke 'derivatives': we all know that constants have derivative 0, and constants are the things that "don't depend" on anything else. The problem here is that this presumes real-valuedness, continuity, and all sorts of other undesirable things. We can do better.

Let's say that a function $f : X \rightarrow Y$ *is independent of* $X$ if $\forall x,y : X\ . f(x) = f(y)$. In other words, $f$ does not depend on its input at all. This definition only needs evaluation, equality, and universal quantification to make sense. Very weak requirements indeed!

That definition is about independence, not dependence. As we'd like to be constructive (if possible), let's say that $f : X \rightarrow Y$ *can be shown to depend on* $X$ if $\Sigma x,y : X\ . \neg (f(x) = f(y))$, i.e. we can exhibit a pair of values of $X$ that evaluate (under $f$) to different values. 

But if we look at many of the examples given, we can see that this doesn't capture anywhere close to the right ideas. Again, an example: pick $f : \mathbb{R} \rightarrow \mathbb{R}$ as $f(x) = \sin(x)^2+\cos(x)^2$. Does $f$ *depend on* $x$? Does $f$ *depend on* $\sin$ and $\cos$? Using our mathematical definition, $f$ does not depend on $x$. But if you implement it using floating point, it will. In many ways, this is a spurious example, because the 'implements' relation here is not faithful. However, the other question remains: does $f$ depend on $\sin$? That is a perfectly legitimate question, but it is being asked naively. First, the question doesn't even "type check". Neither $\sin$ nor $\cos$ are in $\mathbb{R}$! What we're doing in that question is mixing syntax and semantics.

Stuff to still write about
- syntax and semantics
- observations
- allowed changes
