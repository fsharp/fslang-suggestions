# Support FSharpType and FSharpValue methods on all profiles [14264544] #

**Submitted by Don Syme on 5/27/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

The following functions are missing from FSharp.Core reflection support for Profile78, 259 and .NET Core. This is because the “BindingFlags” type is not available in those profiles.
type FSharpValue =
static member MakeRecord: recordType:Type * values:obj [] * ?bindingFlags:BindingFlags -> obj
static member GetRecordFields: record:obj * ?bindingFlags:BindingFlags -> obj[]
static member PreComputeRecordReader : recordType:Type * ?bindingFlags:BindingFlags -> (obj -> obj[])
static member PreComputeRecordConstructor : recordType:Type * ?bindingFlags:BindingFlags -> (obj[] -> obj)
static member PreComputeRecordConstructorInfo: recordType:Type * ?bindingFlags:BindingFlags -> ConstructorInfo
static member MakeUnion: unionCase:UnionCaseInfo * args:obj [] * ?bindingFlags:BindingFlags -> obj
static member GetUnionFields: value:obj * unionType:Type * ?bindingFlags:BindingFlags -> UnionCaseInfo * obj []
static member PreComputeUnionTagReader : unionType:Type * ?bindingFlags:BindingFlags -> (obj -> int)
static member PreComputeUnionTagMemberInfo : unionType:Type * ?bindingFlags:BindingFlags -> MemberInfo
static member PreComputeUnionReader : unionCase:UnionCaseInfo * ?bindingFlags:BindingFlags -> (obj -> obj[])
static member PreComputeUnionConstructor : unionCase:UnionCaseInfo * ?bindingFlags:BindingFlags -> (obj[] -> obj)
static member PreComputeUnionConstructorInfo: unionCase:UnionCaseInfo * ?bindingFlags:BindingFlags -> MethodInfo
static member GetExceptionFields: exn:obj * ?bindingFlags:BindingFlags -> obj[]
type FSharpType =
static member GetRecordFields: recordType:Type * ?bindingFlags:BindingFlags -> PropertyInfo[]
static member GetUnionCases: unionType:Type * ?bindingFlags:BindingFlags -> UnionCaseInfo[]
static member IsRecord: typ:Type * ?bindingFlags:BindingFlags -> bool
static member IsUnion: typ:Type * ?bindingFlags:BindingFlags -> bool
static member GetExceptionFields: exceptionType:Type * ?bindingFlags:BindingFlags -> PropertyInfo[]
static member IsExceptionRepresentation: exceptionType:Type * ?bindingFlags:BindingFlags -> bool
These functions are really part of the basic F# programming model. This is a frustrating problem because the “BindingFlags” is really only used to supportBindingFlags.NonPublic, and could always just as well have been a Boolean flag.
I believe we should really make alternative versions of these available, especially on .NET Core but also on the portable profiles.



## Response ##
** by fslang-admin on 6/13/2016 12:00:00 AM **

Completed per comment
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14264544)**


## Comments ##


#### Comment by Don Syme on 6/13/2016 5:48:00 AM ####
This has actually already been done as part of F# portable profile work https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1013-enable-reflection-functionality-on-portable-profiles.md

