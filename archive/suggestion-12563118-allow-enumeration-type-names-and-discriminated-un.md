# Allow enumeration type names and discriminated union type names in a for loop (from Ada 2012) [12563118] #

**Submitted by Alexei Odeychuk on 3/2/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

I suggest using enumeration type names and discriminated union type names in a for loop meaning to try every value (from Ada 2012).
For example,
a) Enumeration type name in a for loop:
type Animals =
| Tiger = 1
| Cat = 2
| Lion = 3
for animal in Animals do printf "%A" animal
As of today, the F# compiler posts a message: error FS0039: The value or constructor 'Animals' is not defined.
b) Discriminated union type name in a for loop (Ada 2012 does not have discriminated union types, but it has record types with a discriminant (parameter) that resemble discriminated union behavior, but they have completely different syntax):
type Animals = Tiger | Cat | Lion
for animal in Animals do printf "%A" animal
As of today, the F# compiler posts a message: error FS0693: The type '(unit -> Animals)' is not a type whose values can be enumerated with this syntax, i.e. is not compatible with either seq<_>, IEnumerable<_> or IEnumerable and does not have a GetEnumerator method
c) For loop can be applied to generate a list, sequence etc., for example:
type Animals = Tiger | Cat | Lion
let animalSequence =
seq { for animal in Animals -> animal } // seq { Tiger; Cat; Lion }
I think it's a good idea to allow enumeration type names and discriminated union type names in for loops and treat enumeration types and discriminated union types by the F# compiler as types compatible with IEnumerable and having a GetEnumerator method (even if they don't). It will make the F# syntax more expressive and bolster F# competitive strengths.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12563118)**


## Comments ##


#### Comment by Jack Fox on 3/6/2016 11:13:00 AM ####
I see merit in this, but I'm withholding my vote as I would rather see this implemented as the having the standard collection functions (fold, map, etc.) over enumerations and discriminated unions. Then this all becomes composable. For loops are not so composable.


#### Comment by Gauthier Segay on 3/6/2016 9:33:00 PM ####
What is expected error message if any of the DU member has data defined for it?


#### Comment by Alexei Odeychuk on 3/10/2016 9:29:00 AM ####
Gauthier Segay, I think the situation where a discriminated union case has data associated with it should not stand in the way of the introduction of the syntax allowing the usage of discriminated union type names in a for loop. I think there is no need to raise an exception here. The discriminated union is a foundational type in functional programming. So, I suggest default initializing all data fields associated with the appropriate discriminated union case. There is function Unchecked.defaultof<'T> to generate a default value for any type in F#. The compiler can use it to generate compiled code.
If a language user wants to change any default initialized data field associated with a particular union case, this can be done by writing the code snippet like this:
type Animals = Tiger of age : int * name : string | Cat | Lion
[ for animal in Animals ->
match animal with
| Tiger(age, name) -> Tiger(2, Kitty) // change the initial
// default value
| predator -> predator ]
|> List.iter (printfn "%A")
As to a comment by Jack Fox: I believe that the syntax suggested can be implemented in the compiler even without standard collection functions (fold, map, etc.) over enumerations and discriminated unions.
The compiler can obtain information on all union cases defined by a language user for a particular discriminated union type from code (The similar applies to enumeration types). So, the F# compiler can convert the expression "for animal in Animals" to "for animal in seq { yield Tiger(Unchecked.defaultof<int>, Unchecked.defaultof<string>); yield Cat; yield Lion }" behind the scenes in order to reach the goal of the syntax suggested.

