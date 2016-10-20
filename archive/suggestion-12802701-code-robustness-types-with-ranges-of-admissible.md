# Code robustness: Types with ranges of admissible values (from Ada 2012) [12802701] #

**Submitted by Alexei Odeychuk on 3/4/2016 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

I suggest introducing an aspect that can be applied to declarations of enumeration types, discriminated union types and user-defined numeric types with the aim of specifying the range of admissible values for subtypes derived from base types easily.
This suggestion is an extension of my previous suggestions:
1) Types with predicates to create subtypes easily (from Ada 2012);
2) Types with default initial values specified (from Ada 2012).
Please see them for more details:
1) /archive/suggestion-12564486-types-with-predicates-to-create-subtypes-easily-f
2) /archive/suggestion-12800967-types-with-default-initial-values-specified-from
Example # 1. Type with range of admissible values specified.
type scores = int range 1 .. 100 // admissible values: 1, 2, 3 .. 100
The aspect should be checked (checks for admissible values should be generated in compiled code by the F# compiler and performed) whenever an object of the type is default initialized, on assignments, on type casts, on parameter passing, in the match expressions and so on.
Example # 2: Type with range of admissible values and default initial value.
type rating =
| A
| B
| C
| D
| E
| F
type goodRating = rating range A .. C default A
Example # 3: Type with range of admissible values, default initial value and subtype predicate.
// admissible values of the type: 0, 2, 4, 6, 8 .. 100
Syntax version # 1:
type Even = int range 0 .. 100 default 0 with function
| n when n % 2 = 0 -> true
| _ -> false
or
Syntax version # 2 (both versions may be acceptable):
type Even = int range 0 .. 100 with default 0 and function
| n when n % 2 = 0 -> true
| _ -> false
This feature would be exceptionally useful when paired with units of measure.
Example # 4: Type with unit of measure, range of admissible values, and default initial value.
[<Measure>]
type celsius
Syntax version # 1:
type temperature = float<celsius> range -80.0<_> .. 60.0<_> default 0.0<_>
or
Syntax version # 2 (both versions may be acceptable):
type temperature = float<celsius> range -80.0<celsius> .. 60.0<celsius> default 0.0<celsius>
This change in the F# language syntax will not affect existing codebase. It requires introducing a new keyword: range. I think this syntax will help represent a programmer's intents in code and improve code robustness and expressiveness of the F# language.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12802701)**


## Comments ##

