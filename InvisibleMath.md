Proof assistants offer an interesting opportunity: revealing "invisible math", giving us a way to better understand what paper mathematics keeps implicit. This better understanding can then be used to create better features to make it implicit also in formalized versions, at least when there is a disciplined, reasoned way to do so. I consider the vast majority of current features that try to do automation to be reactionary hacks that attempt to mimic human mathematics without deeply understanding what's really going on. 

For example, it is possible to use latex as a mere word processor. In this mode of usage, latex is actually a major pain. But if you more deeply understand the features of latex, you can start to modify how you write papers to take advantage of these features. Slowly, it becomes quite reasonable to use latex. In many ways, this is what a lot of latex packages represent: an encoding of human knowledge that helps improve the *process* of math-heavy document writing.

One of the most obvious advances that has been facilitated by proof assistants is the realization amongst mathematicians that "equality" is not so simple, and that there's a lot more to it, isomorphism and notions of 'canonical' than the literature seemed to say. It's also amusing that, upon reflection, Grothendieck already knew this, and you can see it in his writing going back to the mid 1950s. Proof assistants being a royal pain about equality is a symptom that this is a difficult issue, not something to beat down and bury!!!

Namespaces is another such symptom. Mathematics is huge and much too often uses similar notation for wildly different things. Humans struggle with this, but machines even more. We should learn from this instead of trying to bury it. In particular, we should learn that being precise about the stuff that is "implicitly assumed to be visible" at any given point in a mathematical development is quite useful. That it is a fair amount of work to do so should inform us on the struggles of learners. Just because successful people are able to juggle all of this in their head doesn't mean that it should be a required skill of all future mathematicians! That becomes an exclusionary mechanism that may rule out superb problem solvers who struggle to keep large amounts of theory in their active brains.

Even super simple things like "Let G be a Group" hides enormous complexity that we should be aware of: this 'speech act' in mathematics actually brings into scope
- a bunch of names (a binary operation, a constant, a unary operation, the names of several proofs)
- a bunch of theorems (you have a Group in scope, so its basic properties are implicitly assumed too)
- a bunch of definitions and constructions And so on. That's way too much for so few words. And wildly imprecise!

No wonder our computers struggle like mad when we say "Let G be a Group and M a Monoid". We've just brought into scope a bunch of conflicting things. The usual reply is "it's ok, it can all be resolved uniquely". But this is complete BS: it can only be resolved uniquely when you know a priori that the statement you've made next is correct. If you've made a mistake, then all hell breaks loose, it is no longer unique. So our language for doing mathematics is extremely unhelpful and fragile with respect to errors.

I could go on and on. Proof assistants are wonderful in this respect: they are very revelatory of the 'badness' embedded in mathematical vernacular.
