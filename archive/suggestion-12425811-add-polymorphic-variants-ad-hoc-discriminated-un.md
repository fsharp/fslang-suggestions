# Add Polymorphic Variants (ad-hoc Discriminated Unions) [12425811] #

**Submitted by Jared Hester on 2/21/2016 12:00:00 AM**  
**36 votes on UserVoice prior to migration**  

Creating strongly typed data constructs with some level of heterogeneity is often accomplished with DUs so lets take the trivial case of wanting
to have lists of floats & ints, ints & strings, and ints & floats & strings
We'd need the types -
type IntString =
| Int of int
| String' of string
type FloatInt =
| Float of int
| Int of int

type IntFloatString =
| Float of int
| Int of int
| String' of string
But in practice using these would require qualified access to make sure you're getting the right case from the right type and as types you
want to group grow in number there's a combinatory explosion of boilerplate and verbose code necessary to put it to work.
Polymorphic variants cut down the noise and increase the flexibility and expressiveness of your code.
The declaration of a polymorphic variant in OCaml is not unlike that of the single case DUs that are already commonly found in F# code
Instead of -
type Int = Int of int;;
> type Int = | Int of int
Int 3;;
> val it : Int = Int 3
OCaml and uses a preceding backtick convention for a simplified syntax-
let three = `Int 3;;
> val three : [> `Int of int ] = `Int 3
let four = `Float 4.;;
> val four : [> `Float of float ] = `Float 4.
The `>` at the beginning of the variant types above marks the types as being open to combination with other variant types.
Which means a list could be declared as such -
let ls = [three; four]
> val ls : [> `Int of int | `Float of float]
and the type would be an ad-hoc Discriminated Union where its cases match the polymorphic variants used
this also applies to function declarations
let is_positive = function
| `Int x -> x > 0
| `Float x -> x > 0.
;;
> val is_positive : [< `Float of float | `Int of int ] -> bool = <fun>
The `<` is there because is_positive has no way of dealing with values that have tags other than `Float of float or `Int of int.
The `<` and `>` markers are indicators of the upper and lower bounds on the tags involved.
If the same set of tags are both an upper and a lower bound, we end up with an exact polymorphic variant type, which has neither marker
let exact = List.filter is_positive [three;four];;
> val exact : [ `Float of float | `Int of int ] list = [`Int 3; `Float 4.]
^ summarizing the part of Real World Ocaml on Polymorphic Variants
https://realworldocaml.org/v1/en/html/variants.html
further reference - http://caml.inria.fr/pub/docs/manual-ocaml-400/manual006.html#toc36



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12425811)**


## Comments ##


#### Comment by Jack Fox on 3/6/2016 11:36:00 AM ####
Would there be a single ad-hoc Discriminated Union for all polymorphic variants currently in scope? Then depending on program structure and scope different sets of polymorphic variants would be available.
I think I like this idea...

