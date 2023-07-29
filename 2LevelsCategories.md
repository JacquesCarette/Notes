Right now, every component in a category (there are 3 in agda-categories, namely objects, morphisms and morphism equivalence) are supposed to live at a single level / belong to a single universe. But what if we knew that some of theses were compose of 'items' which lived in a (fixed, finite, given) set of levels?

The first thing to explore would be to do this for 2 levels, i.e. where all 3 parts could have pieces from 2 universes.

Slice categories offer a first test case, and the coslice and comma.

An obvious generalization would be an IJK-category. In fact, comma categories are probably 221-categories in that sense.

These seems to be deeply related to Displayed Categories! Right now, I've started [doodling around](2Level/Category.lagda) on this.
