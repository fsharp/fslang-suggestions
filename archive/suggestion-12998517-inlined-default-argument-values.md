# Inlined default argument values [12998517] #

**Submitted by Vasily Kirichenko on 3/17/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Instead of
member __.Foo(?a: int) =
let a = defaultArg a 2
it would be great to write it C#-slyle:
member __.Foo(?a: int = 2)



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12998517)**


## Comments ##


#### Comment by Alexei Odeychuk on 3/17/2016 12:13:00 PM ####
I agree with Vasily, but I think the "?" symbol is not necessary at all for the syntax suggested. In my opinion, that symbol has no value added; it worsens the readability of code only.
I think it would be even better to write it in the VB.NET or Ada 2012 style:
member _.Foo(a : int = 2).
Sidenote: the value "a" has to belong to type int during all its lifetime (as declared in a member or function).
For example,
member ___.Foo(a : int = 2): int =
(*…….……*) if a = 2 then 0 else a
For the sake of the F# language stability, let the two syntax models co-exist. Let the "member __.Foo(?a: int)" syntax remain in the existing codebase, and let's open opportunities for the new syntax "member _.Foo(a : int = 2)" to become widely used in new code!

