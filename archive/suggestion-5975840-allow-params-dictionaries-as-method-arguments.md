# Allow "params" dictionaries as method arguments [5975840] #

**Submitted by Tomas Petricek on 5/27/2014 12:00:00 AM**  
**30 votes on UserVoice prior to migration**  

When interoperating with languages that are more dynamic than F# (like Python, Matlab or R), we can often get the list of available methods/functions, but we cannot always get the names and types of parameters. For example, in R provider, you sometimes have to write:
namedParams [ ("xval", days), ("yval", prices), ("another", box 1) ]
|> R.plot
It would be nice if I could put the "Params" attribute on a "IDictionary<string, 'T>" and let the compiler provide all additional named parameters as a dictionary:
R.plot(xval=days, yval=prices, another=1)
This would have other uses - for example, when creating a Deedle data frame, you need to specify names of columns. We have a custom operator and function for that:
frame [ "prices" => prices; "days" => days ]
But with the new feature, we could let you write, for example:
Frame.ofColumns(prices = [...], days, = [...])
This could really be done just by adding [Params] attribute to an IDicitionary parameter. To support the R provider case, this needs to work in type providers too.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

Updating to planned to indicate this is approved in general terms. A detailed design and implementation would be needed.
Implementations of approved language design can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5975840)**


## Comments ##


#### Comment by Tomas Petricek on 5/27/2014 12:02:00 PM ####
Just for a reference, I imagine that the definition would look like this:
type R =
static member plot([<Params>] args:IDictionary<string, obj>) = (...)
I suppose one subtle thing here is to make sure that the type information propagates correctly through the type inference - so when you define it as taking `obj`, the arguments will need to be boxed, but when you define the dictionary as containing just `float` values, the optional arguments would presumably be restricted to floats.


#### Comment by Richard Minerich on 5/27/2014 2:12:00 PM ####
It also should be noted that IDictionary does not have an ordering while the arguments do. It would be ideal to capture this information.


#### Comment by Don Syme on 6/20/2014 11:46:00 AM ####
I'm generally in favour of addressing this for F# 4.0, if a technically feasible design is proposed, analyzed in detail, and an implementation+testing provided by the F# Community.
To get more concrete, what's being proposed is presumably a new attribute ParamDictionary used like this:
open System
open System.Collections.Generic
open System.Runtime.CompilerServices
type C() =
static member DoSomething1([<ParamArray>] args: 'T[]) = ()
static member DoSomething2([<ParamDictionary>] args: IDictionary<string,obj>) = ()
C.DoSomething2(arg1=1, arg2=3)
Is that correct?
Implementing this is non-trivial (Tomas mentions some reasons why) and libraries would pick up a dependency on the updated FSharp.Core containing the attribute.


#### Comment by Jack Pappas on 7/6/2014 9:42:00 AM ####
I don't know about the user-facing side of things (i.e., how to expose this in the language), but on the compiled side of things, you could represent this using the usual [<ParamArray>] attribute with a KeyValuePair<string,obj>[]-typed parameter. That would avoid the need for consuming code to take a dependency on FSharp.Core and it would preserve parameter ordering (as Rick mentioned). Although this doesn't actually use IDictionary<_,_>, it doesn't seem likely that most real-world uses are going to pass in more than, say, 20-30 arguments, so lookups can use a linear scan of the argument array to find a matching k-v pair without too much performance overhead.


#### Comment by Jack Pappas on 7/6/2014 9:48:00 AM ####
Another way to implement this (besides what I mentioned below) would be to have a [<ParamDictionary>] attribute and have the F# compiler compile that parameter into an ExpandoObject. That would interop a bit more closely with C# dynamic and the DLR, but the price is that it wouldn't work if targeting a .NET Framework earlier than 4.0.

