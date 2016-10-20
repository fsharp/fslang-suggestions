# Allow type providers to generate types from other types [5675977] #

**Submitted by Tracy on 3/24/2014 12:00:00 AM**  
**116 votes on UserVoice prior to migration**  

There are occasions where it would be extremely useful to generate types from other types.
As an example, F# interop with NHibernate is very clumsy simply because it's difficult to express types of the sort:
// C# record class
public class MyRecord
{
public virtual int Id { get; set; }
public virtual string Description { get; set; }
// etc...
}
It would be very compelling to be able to represent these as F# record types, but the CIL code generated for F# records is incompatible with NHibernate.
Perhaps it could be possible, using a type provider, to generate the POCO class above from an F# record type of the sort:
type MyRecord = { Id : int, Description : string }
The type could be generated as shown below:
type MyPocoRecord = PocoTypeProvider<MyRecord>()
I understand the difficulty of doing this at compile type.Tomas P actually explained why in a forum post (that I can't seem to find.) However, this sort of problem is the reason by the CLIMutable attribute was created, which as far as I can tell, was hard-coded directly into the F# compiler.
I can see these interop dilemmas becoming more common as F# adoption increases, especially in the enterprise where tools like NHibernate are in widespread use. There ought to be a way to address them without creating one-off CLIMutable-esque attributes per se.
The feature itself would open the door to incredibly powerful metaprogramming opportunities.



## Response ##
** by fslang-admin on 6/24/2016 12:00:00 AM **

Marking this as “approved in principle” per comment below.
However it will be a difficult feature to land in practice and will be subject to very many caveats and likely limitations. There’s no certainty that this will make it into F#.
We will open an RFC for it eventually (it won’t be fast :) )
https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5675977)**


## Comments ##


#### Comment by Bryan Edds on 3/27/2014 9:42:00 PM ####
I think this is very interesting and would love to hear about its advantages and disadvatages from the F# team.


#### Comment by Nicolas R on 5/14/2014 9:28:00 AM ####
This amount to "staged programming" no ? You have to resolve all the types you give as parameters, run the higher level program on that input, and use the result of that in the "normal precedence" program.


#### Comment by trek42 on 6/25/2014 8:27:00 AM ####
We might have a simpler implementation by restricting that the types you give to a type provider must be fully resolved before compiling the current file.
Example:
// in A.fs
type MyRecord = ... // fully defined.
// in B.fs
type ProvidedType = TypeProvider<MyRecord>;
B.fs must go after A.fs, but you can still put B.fs and A.fs in one project and compile them together.
I think this should enable most benefits without resorting to staged programming. Actually, this seems to play quite nicely with the current fsharp compilation model, which already requires fully resolving dependencies before compiling the source file.
(currently you can simulate this feature by compiling A.fs in its own assembly, then give the assembly file path to the type provider. But doing so means you need to split things that should naturally go together into multiple projects, and it quickly become very cumbersome.)


#### Comment by Dave Thomas on 7/2/2014 4:41:00 AM ####
You can already have generative types that inherit from a prescribed type, it would be interesting to extend the syntax so that the prescribed type can be included as a generic argument, or perhaps typeof<'a> in the static arguments.


#### Comment by Don Syme on 2/4/2016 2:01:00 PM ####
I would love to see this feature implemented, it would increase the power of F# type providers immensely.
I will mark this as "approved in principle" and we will eventually open an RFC for it. However it will be a difficult feature to land in practice and will be subject to very many caveats and likely limitations.


#### Comment by Dave Thomas on 4/19/2016 2:40:00 AM ####
One thing that heads towards this is getting intrinsic type extensions working with generative providers. So that you can then create a type from a provider and immediately augment it in some way. RE:https://github.com/Microsoft/visualfsharp/pull/882

