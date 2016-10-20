# DefaultValue attribute should require 'mutable' when used in classes and records [9679206] #

**Submitted by Don Syme on 9/8/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

For structs, adding the DefaultValue attribute to a val declaration (a field) results in a check that the field is mutable, since it doesn't make sense to use an immutable field which only ever has the default value.
[<Struct>]
type S() =
[<DefaultValue>] val x : C
AssemblyReader.fs(4304,23): error FS0880: Uninitialized 'val' fields must be mutable and marked with the '[<DefaultValue>]' attribute. Consider using a 'let' binding instead of a 'val' field.
For some reason, this condition is only checked for fields declared in structs. We should likewise give a warning for records and classes:
type C() =
[<DefaultValue>] val x : C
and
type R = { [<DefaultValue>] x : C; y : int }



## Response ##
** by fslang-admin on 9/8/2015 12:00:00 AM **

Approved for inclusion in a future release of F#.
Please consider contributing to F# by providing an implementation, with adequate testing. The code to be adjusted is around here: https://github.com/fsharp/fsharp/blob/212c3359bf6d83e30c12e53fd2ef283d3257b328/src/fsharp/PostInferenceChecks.fs#L1422. For some reason, the code is only activated for struct/enum type definitions, but it should also apply to record and class type definitions.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9679206)**


## Comments ##

