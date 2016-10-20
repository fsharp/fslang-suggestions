# Length constraints on lists and arrays [6832419] #

**Submitted by Isaac Abraham on 12/11/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Whilst you can pattern match on lists in order to get compiler support on the length of them, it would be great if we had compiler support for list length for e.g. arguments to functions. Things like Seq.head or even list destructuring can't be proven to not go pop except through pattern matching, but if we had the ability to add length constraints to e.g. a list passed in as an argument to a function this would simplify lots of boilerplate code e.g.
let foo(myListOfItems:int list<3>) = () // myListOfItems must be three elements long.
or even
let foo ([ a;b;c;]) = () // automatically unwrap the list of three elements into a b and c.
Not saying that the above syntax would necessarily be the way to go - just ideas as to achieving the aim of getting better compiler support for working with lists.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6832419)**


## Comments ##


#### Comment by Vasily Kirichenko on 12/15/2014 8:03:00 AM ####
As far as I understand this requires dependent types which are very, very unlikely to be added to F# in any observable future.


#### Comment by Daniel Robinson on 12/15/2014 9:53:00 AM ####
Isn't a fixed-length list just a tuple?


#### Comment by Isaac Abraham on 12/26/2014 11:23:00 AM ####
@Vasily - I know diddly about writing compilers :-) But can this not be done with things like units of measure i.e. metadata that gets erased at runtime; could this not be done in a similar manner?
@Daniel - not really - you can't use all the list or sequence operations etc. on them.


#### Comment by Richard Gibson on 1/15/2015 6:06:00 AM ####
You could write a function now to currently turn a tuple of identical items into a sequence, such as:
let asSeq (one, two, three) = seq { yield one; yield two; yield three }
Perhaps you could use a type provider to generate useful functions or extension methods for you.
As for language support, perhaps it would be better to try and get special support from the compiler to let you treat Tuple<T, T, T, ...> as seq<T>.


#### Comment by Craig Stuntz on 3/16/2015 9:42:00 PM ####
You indeed need dependent types for constraints on cardinal length, but some really useful special cases which don't quite require dependent types are lists of length 0 and 1. Here's a Haskell solution for >0 which doesn't require dependent types:
https://wiki.haskell.org/Non-empty_list


#### Comment by Don Syme on 7/17/2015 9:29:00 AM ####
It is possible to deal with some special cases via integer parameters or other existing uses of constraint solving. However that can lead the programmer to use the feature during problem exploration, but then the feature falls down at some point. The programmer must then back out and remove the use of the feature.

