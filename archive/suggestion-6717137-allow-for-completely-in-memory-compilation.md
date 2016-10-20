# Allow for completely in-memory compilation [6717137] #

**Submitted by Aleksander Heintz on 11/14/2014 12:00:00 AM**  
**195 votes on UserVoice prior to migration**  

With the introduction of Roslyn and ASP.Net 5 code is being compiled in-memory and on demand. This allows for drastically reduced compilation times (in some cases there is no disk IO at all). I've written a provider for F# to be used in ASP.NET 5 (it can be found at https://github.com/YoloDev/YoloDev.FSharp.AspNet), which uses `FSharp.Compiler.Service` to do the compilation.
Now, there are several problems with the way it works today.
1. Iit can't run on .NET Core due to the fact that `FSharp.Compiler.Service` doesn't.
2. The compiler does not have any real (that I could figure out at least) API. If you read the code for the FSharp Asp .NET 5 provider, you'll see that it builds up a list of compiler arguments as strings. In Roslyn, you build up syntax trees, and metadata references, and then hand those to a "compilation" which does the work of compiling your code, whereas the F# compiler as of today takes a list of strings which are options and filenames, and then parses those strings (which could have just been option values) and goes and reads the files (which in many cases I just wrote to disk to enable the F# compiler to find them) and then produces an assembly on disk (which I don't need). Now, the `FSharp.Compiler.Service` project has managed to enable me to reduce the amount of IO I have to do by shimming the file-system (with a global state variable, which makes me have to lock the whole compilation process to ensure thread safety) and in theory it should be able to compile to a dynamic assembly however that doesn't work for some reason. Which brings me to my next point:
3. It does not allow for in memory (only) compilation.
My suggestion is to follow the Roslyn model. Build up a Compilation object consisting of SyntaxTrees, MetadataReferences and some options. And have apis for creating the assembly to a stream, instead of just to disk.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Duplicate, see https://github.com/fsharp/FSharp.Compiler.Service/issues/266
which covers the ongoing work for this feature.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6717137)**


## Comments ##


#### Comment by Aleksander Heintz on 11/14/2014 6:35:00 AM ####
Also, (as it seems I can't, or can't figure out how at least), would an admin kindly change the title to "Create a better compiler API"?


#### Comment by David Karlaš on 11/14/2014 12:34:00 PM ####
If TypeScript got Roslyn support... Shouldn't F# too?
http://blogs.msdn.com/b/typescript/archive/2014/11/12/announcing-typescript-1-3.aspx


#### Comment by Don Syme on 11/14/2014 5:22:00 PM ####
Please add suggestions about FSharp.Compiler.Service at https://github.com/fsharp/FSharp.Compiler.Service/.
The FCS API is being improved all the time - for example recently functionality to take an AST and compile it was added by Nessos. So part of what you want is there. You can certainly implement all of the above as relatively simple improvements and simplifications to the current API.
If you need a hand, then people (myself, Anh-Dung Phan, Tomas Petricek and others like the Nessos guys) are here to help.
BTW adding an FCS-Roslyn bridge would be fabulous


#### Comment by Aleksander Heintz on 11/24/2014 6:33:00 PM ####
As I stated in my blog post over at http://alxandr.me/2014/11/23/f-in-asp-net-5-the-good-the-bad-and-the-really-ugly/, I think it's the completely wrong way to go about this. These APIs should be added to the compiler. Not appended on some fork of it that has to be kept in sync manually.


#### Comment by Don Syme on 11/25/2014 9:21:00 AM ####
Hi Alexsander,
Yes, we're aware of that. It is very likely that the F# compiler (including the open edition, the Visual F# compiler and the Visual F# IDE Tools) will eventually be rebuilt on top of the FCS component.
This is a non-trivial task for Visual F# Tools since there are very, very high stability requirements. Also, the Visual F# Tools splits the compiler DLLs into two separate instances (one for compilation, and one smaller part for the language service, to reduce memory footprint of binary sizes a little - an awkward split not needed by other tooling). We'll get there, but we don't want to block all of this: http://fsharp.github.io/FSharp.Compiler.Service/#Projects-using-the-F-Compiler-Services.
So in a sense what you're doing is adding APIs to the likely core component of the _future_ F# compiler. It is the future :)
Roslyn took 5 years to do this, but the process was internal at Microsoft - and I can assure you it was similar. For F#, we're doing the right thing to achieve eventual convergence - while also allowing the F# community to incubate the F# Compiler Service component to be a useful and general component. Using it for ASP.NET vNext is exactly what we need to proof the component at this stage - it's hugely useful to see and support these use cases before we reverse-integrate back into the Visual F# Tools.
If it helps, the process for integrating F# language updates into FCS is simple and just involves a "git pull", since the repos share a common aligned source code history. It's the least of our problems :)
I'd be very glad to talk through all this with you on Skype if you'd like, and to help you with your diffs.
Cheers!
Don
p.s. Some of your criticisms of the F# compiler code are also valid - there is a lot we've been unable to cleanup because we were using a "source drop" model of open source. Applying cleanup is getting easier. And yes, there is lots to do :)


#### Comment by Enrico Sada on 11/17/2015 3:03:00 AM ####
work started, both in fsharp compiler service and visualfsharp
ref https://github.com/fsharp/FSharp.Compiler.Service/issues/266


#### Comment by Don Syme on 2/3/2016 1:46:00 PM ####
This is an FSharp.Compiler.Service feature, as Enrico points out work has started towards its implementation

