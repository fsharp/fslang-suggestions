# Allow type providers to create and provide aliased types [9969741] #

**Submitted by Ben Lappin on 9/29/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

With SqlEnumProvider, unless I create a CLIEnum, the provided type is a module with members of the value's type (e.g. string).
It would be nice to be able to provide a type alias for the members that would be visible from other parts of the program to make clear the association with the provided type (e.g. provided type is named "EmployeeCodes", and the members are strings with aliased type "EmployeeCode").



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Closing because this is already possible today in F# 3.0 and beyond, per my comment below
Thanks for the suggestion.
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9969741)**


## Comments ##


#### Comment by Ben Lappin on 9/29/2015 7:09:00 AM ####
Related suggestion (posted by me):
/archive/suggestion-9969603-make-type-aliases-enforceable-at-compile-time
Stackoverflow question (not posted by me):
http://stackoverflow.com/questions/20567690/can-i-make-multiple-aliases-of-the-same-type-in-an-f-type-provider


#### Comment by Don Syme on 2/4/2016 4:39:00 PM ####
I believe this is actually possible today, though the ProvidedTypes SDK may need updating. Specifically you just have to create a ProvidedSymbolType with the right name and kind. For example
ProvidedSymbolType(ProvidedSymbolKind.FSharpTypeAbbreviation(typeAssembly,typeNamespace, typeName), [])
Certainly the core ITypeProvider mechanism supports this.
I will close this and we can follow up with an issue in https://github.com/fsprojects/FSharp.TypeProviders.StarterPack/

