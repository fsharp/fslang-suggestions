# Allow naming of member constraints [6343928] #

**Submitted by Mark Laws on 8/25/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Static type constraints are rather poorly documented on MSDN; there are few examples, their limitations are not well described (even less so the workarounds), and it's not made clear that you can use them in a manner such as the following example:
module qasd =
type foo = {
quack : int
other : bool
}
type bar = {
quack : int
blah : double
}
type 'a qwop = { quack : int; hooblor : 'a }
let qx = { quack=0; other=true }
let qz = { quack=1; blah=1.0 }
let aa = { quack=2; hooblor="aaaaa" }
let inline m x =
match (^t : (member quack : int) (x)) with // <- HERE
| 0 -> 1
| 1 -> 2
| _ -> 3
let asdfasdfsad = m qx
let aldfjasdk = m qz
let aldcjklz = m aa
The issue is that this doesn't work:
module asdlfjk =
type foo = { quack : int; other : bool }
let qx = { quack=0; other=true }
let inline m (x : ^T when ^T : (member quack : int)) =
match x.quack with
| 0 -> 1
| 1 -> 2
| _ -> 3
let asdfasdfsad = m qx
^T gets constrained to type foo. This is surprising, and the solution is rather unintuitive. I'm not sure if this should be simply a documentation fix (because changing it is incompatible with the existing behavior) or whether some sort of new construct should be introduced.
At any rate, there should be some way of "naming" member constraints so that you don't have to repeat them constantly and to make them easier to invoke.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Closing in favour of suggestions /archive/suggestion-8393964-interfaces-as-simple-reusable-and-named-sets-of-m and /archive/suggestion-8509687-add-constraints-as-a-language-construct


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6343928)**


## Comments ##


#### Comment by exercitus vir on 10/21/2014 7:58:00 AM ####
I would like this idea to be extended to more than one member constraint. That is, I would like to name a set of member constraints. For example:
x : ^T when ^T : (member quack : int) and (member walk : int))
It would be even better if I could name a set of member constraints that would be valid (and enforced) outside of a particular inline function, therefore reusable across many inline functions. For example:
[<Constraints>]
type Duck =
abstract member quack : unit -> int
let inline m (x : ^T when ^T <: Duck) =
match x.quack() with
| 0 -> 1
| 1 -> 2
| _ -> 3


#### Comment by Greg Rosenbaum on 3/16/2015 10:37:00 AM ####
Okay, I've done a writeup on a type system feature called 'inline traits' that replicates this behavior in more concrete terms, with syntax examples. It captures the power of statically resolved member constraints and turns them into a part of the type system.
https://gist.github.com/GregRos/fcc103e777fa13a575bf
An earlier idea of making these things work like interfaces doesn't work well. It either reduces the power of member constraints or makes them break polymorphism in pretty weird ways. As it is, it's a bit weird that conforming to an inline trait isn't inharitable.


#### Comment by exercitus vir on 6/12/2015 6:32:00 PM ####
I have incorporated your suggestion in my suggestion for "Interfaces as simple, reusable and named sets of member constraints on statically resolved type parameters": /archive/suggestion-8393964-interfaces-as-simple-reusable-and-named-sets-of-m


#### Comment by Jared Hester on 6/22/2015 5:32:00 AM ####
Declare them as inline functions -
let inline quackfn x = ( ^t : (member quack : int) x)
let inline m2 x =
match quackfn x with
| 0 -> "zero" | 1 -> "one" | _ -> "two"


#### Comment by Don Syme on 2/3/2016 12:33:00 PM ####
Closing in favour of suggestions /archive/suggestion-8393964-interfaces-as-simple-reusable-and-named-sets-of-m and /archive/suggestion-8509687-add-constraints-as-a-language-construct

