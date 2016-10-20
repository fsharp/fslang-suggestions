# Allow specifying subset of type arguments explicitly [5980924] #

**Submitted by Tomas Petricek on 5/28/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Say we have a generic type Frame<TRow, TColumn>. When using instance methods of the frame, it is possible to write a generic method that takes a single additional type parameter - for example, to get a column as a specific type:
frame.GetColumn<float>("Value")
However, doing the same thing using module and function is not possible, because the corresponding `getCol` function requires three type arguments (TRow, TCol and the additional one):
frame |> Frame.getCol<_, _, float> "Value"
It would be nice if F# had some mechanism that would allow specifying only subset of the type parameters. For example:
let getCol<[<RequiresExplicitTypeArguments>] 'T, 'TCol, 'TRow> frame = (...)
And then I could write just:
frame |> Frame.getCol<float> "Value"
Interestingly, this is also problem for extension methods. When you define a C#-style extension method for a generic type like frame, it also has three type arguments and it is impossible to call it with just a single type argument.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

Updating to planned to indicate this is approved in general terms. A detailed design and implementation would be needed.
Implementations of approved language design can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5980924)**


## Comments ##


#### Comment by Don Syme on 6/20/2014 11:38:00 AM ####
Having seen the impact this problem has on Deedle, I'm in favour of addressing it for F# 4.0. I will mark it "approved" (using the label "planned") as a result, though the details need to be worked out.
Another possible declaration syntax is this:
let getCol< 'T, 'TCol, [<OptionalArgument>] 'TRow > frame = ()
or this
let getCol< 'T, 'TCol, 'TRow? > frame = ()
The former has the downside that it could only be used with an updated FSharp.Core since the Microsoft.FSharp.Core.OptionalAttribute would need to be updated with a flag to say it's permissible to use the attribute here (or the F# 4.0 compiler would need to be adjusted to allow the use of this attribute even if the flag has not been updated, e.g. when using FSharp.Core 4.3.0.0 with F# 4.0 compiler)
We should also now consider what the precise language/spec rules should be. Please list questions to be addressed below.


#### Comment by Gusty on 11/8/2015 2:12:00 AM ####
For completeness it will be nice to allow to use the underscores in the declaration as well.
let func<_> = ()
Currently this is allowed: let func< 'T, .. > = ()
So, this should be allowed too: let func< .. > = ()

