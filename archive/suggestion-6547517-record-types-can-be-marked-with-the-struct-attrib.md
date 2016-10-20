# Record types can be marked with the Struct attribute [6547517] #

**Submitted by Will Smith on 10/10/2014 12:00:00 AM**  
**64 votes on UserVoice prior to migration**  

A simple idea, record types can become structs; effectively, allowing record types to have the performance characteristics of structs.
Example:
[<Struct>]
type Vector3 = { X: float32; Y: float32; Z: float32 }



## Response ##
** by fslang-admin on 6/17/2016 12:00:00 AM **

This feature is approved for inclusion in a future revision of the F# language
The RFC is here: https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1008-struct-records.md
The implementation is almost done, please see the link in the RFC
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6547517)**


## Comments ##


#### Comment by Will Smith on 10/10/2014 4:20:00 PM ####
It was agreed upon that struct records should not be able to call their base ctor.


#### Comment by Will Smith on 10/10/2014 4:21:00 PM ####
https://visualfsharp.codeplex.com/discussions/569437 More Info


#### Comment by Jared Hester on 8/23/2015 3:46:00 AM ####
It'd be fantastic if they supported the `with` keyword for copying


#### Comment by Cameron Taggart on 12/15/2015 11:18:00 AM ####
This suggestion and "short tuples compiled as structs" [1] both regard increasing performance by using structs in certain situations. I would love to know more about which situations this benefits. I think it may be partially answered on stackoverflow.[2] Is there any difference in performance today with records and tuples?
I've been hacking the F# AST lately. It is a discriminated union of tuples [3]. Would there be any performance difference if it was represented as a discriminated union of records? Would making it a discriminated union of struct records change its performance characteristics? I am not suggesting we change it. I'm just using it as an example.
[1] /archive/suggestion-6148669-short-tuples-compiled-as-structs-up-to-25x-per
[2] http://stackoverflow.com/questions/521298/when-to-use-struct
[3] https://github.com/fsharp/fsharp/blob/master/src/fsharp/ast.fs#L415


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 3/2/2016 10:10:00 AM ####
See https://github.com/Microsoft/visualfsharp/pull/620 for the latest implementation


#### Comment by Schmoopy on 5/5/2016 12:36:00 AM ####
This is FANTASTIC. I actually am updating my current base to convert a record to a struct for performance (the small type gets created millions of times which was not initially planned)


#### Comment by exercitus vir on 7/7/2016 7:21:00 AM ####
This is a great idea. Can you add a bit more details what this would be translated to and how it can be used? Is this simply syntactic sugar for declaring an ordinary struct, but being able to use the (much nicer) syntax of records? Does a struct record still have a default non-overridable parameterless constructor? Does it support pattern matching and type inference?


#### Comment by exercitus vir on 7/7/2016 8:10:00 AM ####
This feature has been merged. More information can be found here: https://github.com/Microsoft/visualfsharp/pull/620
It includes the answer to one of my questions: The default non-overridable parameterless constructor of structs exists, but cannot be called from F#. I guess {... with ...}, pattern matching and type inference will also work if this still a record.


#### Comment by exercitus vir on 7/7/2016 8:13:00 AM ####
Cross-reference to single case unions compiled as structs:
- initial feature suggestion: /archive/suggestion-6147144-allow-single-case-unions-to-be-compiled-as-structs
- F# RFC FS-1014: https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1014-struct-unions-single-case.md

