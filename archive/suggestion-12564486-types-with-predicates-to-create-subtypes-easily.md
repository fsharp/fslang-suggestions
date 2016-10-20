# Types with predicates to create subtypes easily (from Ada 2012) [12564486] #

**Submitted by Alexei Odeychuk on 3/2/2016 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

I suggest introducing type predicates as an aspect that can be applied to declarations of enumeration types, discriminated union types and user-defined numeric types with the aim of creating subtypes easily.
Suppose, we are concerned with animal species and that we have a
type Animals thus:
type Animals =
| Tiger
| Lion
| Cat
| Mouse
| Hamster
Now suppose we wish to declare subtypes for predators and prey.
So we would like to declare a type Predators embracing Tiger, Cat and Lion, and a type Prey embracing Mouse and Hamster.
I suggest two ways to do this:
1) We can do this with an anonymous function performing pattern matching (subtype predicate in Ada 2012) by writing:
type Prey = Animals with function
| Mouse
| Hamster -> true
| _ -> false
type Predators = Animals with function Tiger | Cat | Lion -> true
| _ -> false
and then we are assured that objects of type Predators can only be Tiger, Cat or Lion, and objects of type Prey can only be Mouse or Hamster.
Another example:
type Even = int with function
| n when n % 2 = 0 -> true
| _ -> false
The aspect should be checked (checks for admissible values should be generated in compiled code by the F# compiler and performed) whenever an object of the type is default initialized, on assignments, on type casts, on parameter passing, in the match expressions and so on.
2) If we want to use a named function performing pattern matching, then we have to write:
type Animals =
| Tiger
| Lion
| Cat
| Mouse
| Hamster
let isPredator(animal: Animals): bool =
match animal with
| Tiger | Cat | Lion -> true
| _ -> false
type Predator = Animals with isPredator;
And last but not least, types with predicates should be allowed in a for loop meaning to try every value. So F# programmers should be able to write:
for animal in Predators do ...
for digit in Even do ...
Please see my previous suggestions for more details:
a) Allow enumeration type names and discriminated union type names in a for loop (from Ada 2012): /archive/suggestion-12563118-allow-enumeration-type-names-and-discriminated-uni;
b) Allow basic integer numeric type names in a for loop (from Ada 2012): /archive/suggestion-12564057-allow-basic-integer-numeric-type-names-in-a-for-lo
The suggested syntax allows writing clear, concise and easy-to-understand code. It will not affect existing codebase.
I think it will help bolster F# competitive strengths and improve its position in the TIOBE language popularity index.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12564486)**


## Comments ##


#### Comment by NhlCrd on 3/14/2016 4:56:00 PM ####
It is not obvious to me what advantages this feature would provide over active patterns and partial active patterns.
Syntactically speaking, (P)APs are also more concise:
let (|Predator|Prey|) = function
|Tiger|Lion -> Predator
|Mouse -> Prey


#### Comment by OneWingedShark on 3/14/2016 11:25:00 PM ####
Per haps a better demonstration would be user-input or data-validation; here's a couple simple examples using Ada 2012's type-system to ensure formatting/data consistsancy:
https://m.reddit.com/r/programming/comments/2770qx/computer_science_and_math/chz389x
https://m.reddit.com/r/programming/comments/238v7g/three_flaws_in_software_design_part_1_writing/cgv37g7

