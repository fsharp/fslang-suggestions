# Allow inheritance from .NET types that implement the same interface at different generic instantiations [5663504] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**60 votes on UserVoice prior to migration**  

http://stackoverflow.com/questions/1464109/implementing-the-same-interface-at-different-generic-instantiations



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

This has been completed for F# 4.0+
The user voice suggestion has been renamed to reflect the feature implemented – “Allow inheritance from .NET types that implement the same interface at different generic instantiations”
The overall status for F# 4.0 is at https://github.com/Microsoft/visualfsharp/wiki/F%23-4.0-Status
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663504)**


## Comments ##


#### Comment by Andrew Khmylov on 3/21/2014 9:50:00 AM ####
Looks like a quite important feature to me.
We have a fairly sophisticated C# code base which encodes a lot of business rules in type system and heavily uses multiple interface implementations with various type parameters. Converting it to F# is not possible at the moment due to this compiler restriction.


#### Comment by Jack Pappas on 3/23/2014 7:51:00 AM ####
I've run into this a few times. I understand it may be a difficult feature to implement due to type inference (see Brian's answer to the linked StackOverflow question); but as Andrew said, it can be a show-stopping issue when you want to convert an existing C# library to F# but the public API can't be changed.


#### Comment by Aaron Bockover on 8/28/2014 10:46:00 AM ####
We ran into this with a type written in C# implementing multiple IObservable<T> interfaces. Fortunately we were able to change that API design on the C# time by the time we realized we were hosed on the F# side. This would be incredibly useful to support in F#.


#### Comment by Don Syme on 9/16/2014 11:55:00 AM ####
The main problem is an interaction with type inference, where F# makes the assumption that if a type is constrained by both I < T > and I < U > then T = U.
This means it will be likely that there is an ongoing limitation that a type variable can’t be constrained by multiple interface instantiations. However that’s a much weaker restriction than the current one.


#### Comment by Maciej J. Bańkowski on 9/16/2014 2:44:00 PM ####
Don, correct me if I am wrong but the statement
IF type constrained by I < T > and I < U > THEN T = U is simply false and hence is bound to cause problems down the line.
Can this whole assumption be dropped from the compiler?


#### Comment by exercitus vir on 9/17/2014 1:40:00 PM ####
Not fully implementing this feature as in C# makes it rather useless. You must be able to use I<T> and I<U> as interface constraints in F# if I is a generic interface and T and U are type parameters. The following assumption should be dropped from the compiler: _if a type is constrained by both I and I then T = U_
Like Maciej said, this is going to cause problems in any case.


#### Comment by exercitus vir on 11/10/2014 12:45:00 PM ####
I still don't like the restricted version, but the notes (copied from the contribution) are interesting, especially the workaround:
"Note, the change still keeps the restriction that an F# type can itself only implement one instantiation of a generic interface type. For example
type C() =
interface I<int>
interface I<string>
is not allowed. This is partly because of the way interface implementation methods are named in compiled IL (only the prefix "I" is added), and partly because the equivalent object expression form can inculde type unknowns, e.g.
{ interface I<_> with ...
interface I<_> with ...
and we don't want to support this kind of inference, and equally don't want a non-orthogonality between object expressions and class definitions. As a workaround you can always add an extra inherit each type you wish to introduce new interface instantiations, e.g.
type C() =
interface I<int> with ...
type D() =
inherit C()
interface I<string> with ...
"


#### Comment by Abel on 11/4/2015 7:07:00 PM ####
Looks like the implementation of this is broken in VS 2015, or at least it works differently now. Generic implementations with different type parameters are still not possible (which is what the user suggested), and calling such an implementation from a .NET library leads to different results between F# 3 and 4.
See: /archive/suggestion-5663504-allow-to-implement-the-same-interface-at-different, titled "Difference between treatment of ambiguous generic interfaces by F# between VS 2012 and VS 2015 leading to compile errors in the latter"

