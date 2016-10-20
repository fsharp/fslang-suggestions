# Allow a single let to create multiple bindings [5691744] #

**Submitted by Patrick Q on 3/28/2014 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

Because spaces will be removed when this is posted I've used dots in their place.
It can often clutter up code when one needs create a lot of let bindings. My suggestion would be to allow a single let to create a group of bindings.
For instance, instead of this ...
let x = blah
let y = blah
let k = blah
let add a b = a + b
let LT a b = a < b
let addMult a b c = (add a b) * c
match x, y with
| blah -> z
| blah -> add x y
we could use the following ...
let x = blah
.....y = blah
.....k = blah
.....add a b = a + b
.....LT a b = a < b
.....addMult a b c = (add a b) * c
match x, y with
| blah -> z
| blah -> add x y
Implementing this feature would de-clutter code without having to completely remove the let keyword, which is unlikely to be practical.This idea should be doable because the indentation can be used to know the scope of the grouped let bindings.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion. Declined per my comment below
Best regards & thanks again,
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5691744)**


## Comments ##


#### Comment by Daniel Fabian on 3/28/2014 1:35:00 PM ####
not quite the same, but you can use tuple syntax in a few cases. E.g. you could write
let x, y, k = blah, blah, blah


#### Comment by Patrick Q on 3/28/2014 8:03:00 PM ####
Daniel, you correct here. I often do this when faced with a few simple bindings, but this won't work for function bindings. Haskell has a similar capability with its "where" clause.


#### Comment by Gauthier Segay on 3/30/2014 10:08:00 AM ####
Supporting let/in and where from haskell would be even greater
let a =
b =
c =
in
match a;b with
...
match a, b with
...
where
a =
b =


#### Comment by let rec on 3/31/2014 1:16:00 PM ####
Using tuples costs allocation, because the compiler doesn't optimize tuples away.
This http://connect.microsoft.com/VisualStudio/feedback/details/719299/tuple-allocations-are-not-eliminated-for-tuples-constructed-from-implicitly-returned-formal-arguments proposal along with the fix was rejected for some reason.


#### Comment by Will Smith on 3/31/2014 1:33:00 PM ####
let rec,
Not always true, sometimes the compiler does optimize tuples away. It depends on what is going on.


#### Comment by Patrick Q on 6/16/2014 6:59:00 AM ####
To make my original suggestion more practical, may I also suggest that the now rarely unused "in" keyword be made use of when "let" is bound to multiple values as in the following:
let x = blah
.....p, q = List.partition fn stuff
.....k = List.length y
.....add a b = a + b
.....addMult a b c = (add a b) * c
in // NOTE: "in" required when a single "let" is bound to multiple values
match x, y with
| aaa, bbb -> addMult p q k
| ccc, ddd -> add p q


#### Comment by Don Syme on 6/25/2014 7:23:00 AM ####
Hi @letrec - I see the link to your proposed optimization patch for tuples. Please consider submitting this improvement to https://visualfsharp.codeplex.com/, now that contributions are being accepted for the F# compiler and language
Thanks
Don


#### Comment by Don Syme on 2/5/2016 6:57:00 AM ####
I will mark this as declined, since it would introduce multiple ways of doing the same thing into the F# language. See also /archive/suggestion-5681764-make-let-optional which was declined on similar grounds.

