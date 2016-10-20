# Allow implementation of abstract slots with generic return type instantiated at type 'unit' [11356293] #

**Submitted by Eric Stokes on 1/8/2016 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

The behavior described here,
http://stackoverflow.com/questions/26296401/why-is-unit-treated-differently-by-the-f-type-system-when-used-as-a-generic-i
is quite surprising to someone coming from other typed FP languages. The fact that a generic type parameter can't be unit makes the whole generics abstraction feel a bit leaky and hacky, which isn't great publicity, as F# actually has a lot of great ideas.
In practice this comes up when implementing type indexed values of various sorts, as an interface is an ideal and natural way to do that, and of course one often wants to have a sometype<unit> value. The compiler error is rather surprising as well, as it implies the object expression doesn't implement the interface, which of course isn't the case.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Approving this in principle, it would be great to fix this behavior.
We will open an RFC on this in due course, https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
There are reasons for the existing behaviour due to unit v. void, as explained in the various stackoverflow topics on this question, but it should be possible to workaround those.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11356293)**


## Comments ##

