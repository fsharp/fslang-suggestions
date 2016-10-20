# Use the "not in" keyword combination for membership tests (from Ada 2012) [12797964] #

**Submitted by Alexei Odeychuk on 3/4/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I suggest using the "not in" keyword combination for membership tests (from Ada 2012).
Example # 1:
if x not in 1 .. 100 then ... // this form of the if expression has better readability than: if x < 1 || x > 100 then..., and you have no need to use the "x" value name twice.
Example # 2:
match counter with n when n not in 1 .. 10 .. 101 -> ... // the when expression here has a succinct form and better readability than the current syntax: match counter with n when [ 1 .. 10 .. 101 ] |> List.forall (fun x -> x <> n) -> ...
Example # 3:
let x = 0
let testX = x not in 1 .. 5 .. 21 // testX = true because 1 .. 5 .. 21 is the sequence of integers: 1; 6; 11; 16; 21.
I think it's a good, easy-to-implement idea to take this notation from Ada 2012 to bolster competitive strengths of the F# language in the context of writing succinct, easy-to-read and easy-to-understand code.
P.S. This suggestion is an extension of my previous suggestion:
Use the in keyword and "|" symbol for membership tests and better readability (from Ada 2012).
Please see it for more details. These suggestions are interdependent: /archive/suggestion-12560184-use-the-in-keyword-and-symbol-for-membership-t



## Response ##
** by fslang-admin on 3/4/2016 12:00:00 AM **

Thanks for the suggestion. Declined per my comment. Adding new syntax for “not” is not a good fit for the F# language design
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12797964)**


## Comments ##


#### Comment by Don Syme on 3/4/2016 6:55:00 AM ####
Even if the other suggestion were accepted we would use "not (x in 1 .. 21)" in F#.


#### Comment by Alexei Odeychuk on 3/7/2016 2:08:00 PM ####
Don, syntax "not (x in 1 .. 21)" is even better than in Ada. I think syntax like "(x in 1 .. 21 | 100 | 200 .. 300)" and "not (x in 1 .. 21)" will be a good contribution to the expressiveness of F#. I am very much looking forward to a change in the status of my other suggestion (Use the in keyword and "|" symbol for membership tests and better readability, from Ada 2012) to UNDER REVIEW or PLANNED. Thank you very much for your attention to my suggestions aimed at making F# better.

