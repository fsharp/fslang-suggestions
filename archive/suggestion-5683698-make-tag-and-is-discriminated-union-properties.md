# Make .Tag and .Is* discriminated union properties visible from F# [5683698] #

**Submitted by Loic Denuziere on 3/26/2014 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

The .NET class that encodes a discriminated union has `.Is* : bool` properties, for example this:
type Foo = A | B
has the following:
member IsA : bool
member IsB : bool
They are hidden from F#, but they could actually be quite useful. I regularly find myself writing something like this:
List.filter (function A -> true | _ -> false)
when I could write:
List.filter (fun x -> x.IsA)



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

This proposal is “approved in principle” for F# 4.0+. It would make a good addition to F#. (I don’t think the loss of purity (e.g. wr.t. ordering of union cases) is a critical problem and I believe you can turn of the DefaultAugmentation in any case)
Some technical issues may need to be ironed out during implementation.
If this is done, the Tag properties present on these types should also be revealed, that is covered by a separate item.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).
Implementations of approved language design can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library..
I’d be glad to help guide people through the implementation process.
If you strongly think this should not be approved please chime in with your technical feedback.
Thanks
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5683698)**


## Comments ##


#### Comment by Peter Strøiman on 5/13/2014 3:32:00 AM ####
Or even better, have it exposed as static members, so you can write
List.filter Foo.IsA
The latter can work better with some cases of type inference, e.g.
let get<'T> () = instance :?> 'T // instance is declared as an obj
In that case
get () |> List.filter Foo.IsA
Would automatically type infer 'T to be List<Foo>, where
get () |> List.filter (x -> x.IsA)
would not, and thus would not compile


#### Comment by Loic Denuziere on 5/13/2014 4:40:00 AM ####
Peter: The thing is, these methods already exist as instance methods, they're just not exposed in F#. Making them static would break backward compatibility for C# code that uses them.
There is a discussion about a static syntax for instance methods here: /archive/suggestion-5663326-syntax-for-turning-properties-into-functions which would provide the same advantages as you cite, but for all instance methods.


#### Comment by Robert Jeppesen on 6/26/2014 4:12:00 PM ####
I agree with Peter, it would be nice to have this as part of the static type.
We should have both: The static `IsA` would call the instance `IsA`.


#### Comment by Christopher Atkins on 7/17/2014 7:10:00 AM ####
There are a few considerations to take into account when tackling this, per Don Syme:
* The problem is that the generated “Is*” and “New*” for unions are inserted very late in the compilation pipeline, in the “ILX” phase, using nasty code that is somewhat ancient. There are lots of corresponding cases in tc.fs and check.fs to check that the user doesn’t define these him/herself.

* The whole generation of these should probably be lifted up to happen during type checking (the same time we generate compare/equality methods, for example, see augment.fs). Then the “check for duplicates” core would be irrelevant.

* The messiness is compounded by the fact that there are special cases in ILX generation for lists, options and AllowNullValueAsRepresentation unions.


#### Comment by Ovidiu Deac on 10/25/2014 8:03:00 PM ####
Combined with /archive/suggestion-5663326-syntax-for-turning-properties-into-functions would be even nicer:
The code would be:
List.filter Foo.isA

