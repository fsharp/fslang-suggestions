# Use the in keyword and "|" symbol for membership tests and better readability (from Ada 2012) [12560184] #

**Submitted by Alexei Odeychuk on 3/2/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

I suggest using the in keyword for membership tests (from Ada 2012).
Example # 1:
if x in 1 .. 100 then ... // the in keyword would be especially useful within the if expressions. That form of the if expression has better readability than: if x >= 1 && x <= 100 then...
Example # 2:
match counter with n when n in 1 .. 10 .. 101 -> ... // the when expression here has a succinct form and better readability than the current syntax: match counter with n when [ 1 .. 10 .. 101 ] |> List.exists (fun x -> x = n) -> ...
Example # 3:
let x = 21
let testX = x in 1 .. 5 .. 21 // testX = true because 1 .. 5 .. 21 is the sequence of integers: 1; 6; 11; 16; 21.
Interdependent suggestion (from Ada 2012):
I suggest using "I" symbol along with the in keyword for membership tests, for example:
type Animals =
| Dog
| Cat
| Mouse
| Chinchilla
let mutable pet = Chinchilla
if pet in Dog | Cat then ... // if pet = Dog || pet = Cat then ...
The same role for "I" has already assigned within the match expressions in F#:
match pet with
| Dog | Cat -> ...
Moreover, the "I" symbol can be used in F#:
a) for specifying ranges, generating lists, sequences, arrays etc., for example: let lst = [ 1 .. 2 .. 100 | 200 | 1000 .. 3 .. 5000 ];
b) for membership tests (if n in 1 .. 2 .. 100 | 200 | 1000 .. 3 .. 5000 then ...);
c) and within the for loops (for i in 1 .. 2 .. 100 | 200 | 1000 .. 5000 do ... // i is changed from 1 to 99, then becomes equal to 200, then is changed from 1000 to 5000). It's a succinct and easy-to-read notation.
I think it's a good idea to take this notation from Ada 2012 to bolster competitive strengths and popularity of the F# language.
P.S. Ada 2012 is a statically typed, imperative, object-oriented programming language offering extremely strong typing, explicit concurrency, tasks (named and anonymous task types), synchronous message passing between task entries, protected (armored) objects for mutual exclusion. It designed for code readability, safety and maintainability of large, long-lived, mission-critical, safety-critical and security-critical applications. Ada 2012 is the latest version of the Ada language.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12560184)**


## Comments ##

