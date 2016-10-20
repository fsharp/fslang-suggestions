# Allow parameterless constructors in structs [6673905] #

**Submitted by Daniel Robinson on 11/6/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

This will simplify the somewhat arcane rules of struct initialization and provide greater parity with class definition syntax. This StackOverflow question (http://stackoverflow.com/questions/12600574/argument-validation-in-f-struct-constructor/12603786#12603786) illustrates the counterintuitiveness of validating constructor args.
[<Struct>]
type S1 =
val M : int
new(m) =
{ M = m }
then if m < 0 then invalidArg "m" "negative"
would become:
[<Struct>]
type S2(m) =
do if m < 0 then invalidArg "m" "negative"
member val M = m
A similar change is planned for C# 6.0 (https://roslyn.codeplex.com/discussions/562559).
This would open the door to let/do bindings and auto-properties in structs. As noted in the C# discussion, it requires more precise usage of Unchecked.defaultof<T> vs. new T().



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Thanks for the suggestion. See comment below about this feature being pulled from C# 6.0.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6673905)**


## Comments ##


#### Comment by Don Syme on 2/10/2016 10:58:00 AM ####
C# eventually pulled this feature out of C# 6.0. I think we should not do it in F# for that reason alone.

