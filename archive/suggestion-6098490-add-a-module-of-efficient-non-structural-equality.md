# Add a module of efficient non-structural equality/comparison operators [6098490] #

**Submitted by fsharporg-lang on 6/25/2014 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

In F# 3.x uses of =, <>, <, >, <=, >=, compare, max and min use “structural equality and comparison”. This is the right default for a functional data-oriented language.
However, this gives rise to problems because
(a) the .NET op_Equality, op_LessThan and other corresponding static methods are not easily accessible from F#.
(b) the use of F#'s structural equality and comparison can be slow for user-defined value types.
In F# 4.0, it is reasonable to add a module NonStructuralOperators to FSharp.Core which gives an implementation of non-structural equality/comparison operators. Opening this module will ensure these operators are used within that scope, similar to the “Checked” module.



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

Completed for F# 4.0, See https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7675
Don Syme, F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6098490)**


## Comments ##


#### Comment by Alfonso Garcia-Caro on 9/7/2014 9:03:00 AM ####
Operator overloading has always posed a risk to the readability of the code. I'm not sure if it's a good idea to make it too easy to change the behaviour of common operators. The Checked module adds extra checks but doesn't change the intrinsic behaviour of the operators.
I would be in favour of giving easier access to .NET comparison methods but in a way that this is more explicit to the future reader of the code.


#### Comment by Don Syme on 11/11/2014 5:40:00 AM ####
An implementation of a NonStructuralComparison module is here: https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7675


#### Comment by Matthew Peacock on 4/30/2015 9:09:00 PM ####
This addresses a serious problem faced when using F# for time series analysis: the default comparison operators for DateTime and TimeSpan are very slow, and always show up as hot spots under the profiler. However, unless I'm mistaken, this change doesn't help when using these types in collections (for example, Set<DateTime> and Map<DateTime,_> will still be slow), or when calling various methods that do comparison (such as sort, groupBy, partition, etc)?


#### Comment by Paul Westcott on 7/29/2015 2:23:00 PM ####
@Matthew,
https://github.com/Microsoft/visualfsharp/pull/513 changes addresses your concerns. Maybe f# 5?
Cheer,
Paul.

