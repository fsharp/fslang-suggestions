# Add a function to return a constant value [8065539] #

**Submitted by Mark Seemann on 5/21/2015 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

Sometimes, you have to pass a function to a higher-order function, but you want that function to always return the same value, so you may end up writing something like
let ploeh = myHigherOrderFunction (fun _ -> 42) "Foo"
It would be nice with a built-in function that does this, sort of a dual of the built-in 'ignore' function.
Something like
let konst x _ = x
which would enable you to write something like
let fnaah = myHigherOrderFunction (konst 1337) "Bar"



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

Many thanks for the suggestion
I’m declining this because we did explicitly consider this in F# 1.0 (and also F# 4.0) and decided against adding a function to the prelude for this. I don’t think we should revisit that decision at this point.
The Operators prelude is a space of names we have to use somewhat conservatively. The name “konst” is not particularly pleasing, and the function is very, very simple to define as a helper function. So in balance we decided not to include this.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8065539)**


## Comments ##


#### Comment by Daniel Robinson on 5/21/2015 10:40:00 AM ####
Like the idea, but suggest naming it 'constant'. konst smells like something from KDE.


#### Comment by Daniel Robinson on 5/21/2015 10:43:00 AM ####
If 'constant' is too long, 'always' also reads nicely.


#### Comment by Dax Fohl on 5/23/2015 9:03:00 AM ####
All the better if we could make this independent of argument count. https://clojuredocs.org/clojure.core/constantly


#### Comment by Frank Shearar on 5/27/2015 3:31:00 AM ####
@Dax Clojure's constantly (and Common Lisp's CONSTANTLY) only takes one argument. Its _returned function_ takes any number of arguments.
A naive implementation might look like
let constantly x = fun ([<System.ParamArray>] ignored) -> x


#### Comment by Don Syme on 7/17/2015 6:54:00 AM ####
Since it is so easy to define this function as a utility in your own code I'm not sure we need have it in the F# library.
This is consistent to the design approach we've take to a number of other functionals, e.g. swapping the elements of a tuple, or a function to do pointwise "and" and "or" on two Boolean-valued functions.

