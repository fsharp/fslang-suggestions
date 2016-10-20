# Allow provided types to be non-nullable by specifying AllowNullLiteralAttribute(false) [5841349] #

**Submitted by Gustavo Guerra on 4/27/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

As we can only generate classes in type providers and not records, it would be at least very useful to be able to tell the compiler to not allow to use the null literal.
Currently in FSharp.Data, when using the write api for Json and Xml, there's no way to prevent the user to pass null in the constructor of a non-optional parameter, and it would be nice to be able to do that



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

This has been completed for F# 4.0+, see https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/NonNullProvidedTypesDesignAndSpec.md


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5841349)**


## Comments ##


#### Comment by Gustavo Guerra on 4/27/2014 11:07:00 AM ####
I'm thinking about erased type providers here, for generated it's probably not going to be that easy, as they are real classes, but for erased they aren't real classes, so maybe this can be doable


#### Comment by Don Syme on 6/24/2014 11:45:00 AM ####
This is a very reasonable request. Although it needs protoyping and testing, I consider it basically approved. Comments and feedback welcome.
I believe the design would simply be
1. Allow the type provider to specify AllowNullLiteralAttribute(false) as a provided attribute of the provided type definition.
2. The onus is on the type provider to make sure the implied non-nullness contract is satisfied.
Thanks
Don


#### Comment by Don Syme on 6/24/2014 11:45:00 AM ####
I actually have a prototype implementation adjusting TypeNullIsExtraValue (approx code below - this requires some fiddling around putting things in the right compilation order in tastops.fs). I could submit some initial dev testing too. Gustavo, would you be interested in providing review and extra testing for this if i submit it to the F# 4.0 branch?
Thanks
Don
let TypeNullIsExtraValue m g ty =
if isILReferenceTy g ty || isDelegateTy g ty then
// Putting AllowNullLiteralAttribute(false) on an IL or provided type means 'null' can't be used with that type
not (isAppTy g ty && TryFindTyconRefBoolAttribute g m g.attrib_AllowNullLiteralAttribute (tcrefOfAppTy g ty) = Some(false))
elif TypeNullNever g ty then false
else
// Putting AllowNullLiteralAttribute(true) on an F# type means 'null' can be used with that type
isAppTy g ty && TryFindTyconRefBoolAttribute g m g.attrib_AllowNullLiteralAttribute (tcrefOfAppTy g ty) = Some(true))


#### Comment by Gustavo Guerra on 6/24/2014 1:09:00 PM ####
Yes, I can help test. I like the attribute approach as it allows to have the same code base for F# 3.1 and 4.0, 3.1 will just ignore it, if I got it right


#### Comment by Dave Thomas on 7/6/2014 3:50:00 AM ####
In the proposed implementation, other uses are described that mention the use named arguments, will this be expanded upon?


#### Comment by Don Syme on 7/7/2014 9:55:00 AM ####
Hi Dave,
That comment is really just about an internal implementation detail.
Cheers
Don


#### Comment by Don Syme on 1/16/2015 10:48:00 AM ####
A speclet for this feature is here: https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/NonNullProvidedTypes.md

