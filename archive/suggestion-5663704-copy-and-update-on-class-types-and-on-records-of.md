# Copy-and-update on class types and on records of different types. [5663704] #

**Submitted by Don Syme on 3/21/2014 12:00:00 AM**  
**25 votes on UserVoice prior to migration**  

People sometimes find it hard to transition from records to class types - something which comes up when seeking to encapsulate some of the details of the record type.
One particular reason for this is because their codebase may uses copy-and-update on record types. One approach to easing the transition would be to support copy-and-update on class types, as long as the class type follows a particular design pattern.
One pattern-based approach could permit both normal record syntax and copy-and-update syntax, e.g.
[<RecordSyntax>]
type R(a:int, b:int) =
member x.A = a
member x.B = b
member x.C = f(a,b)
with
{ a = e1; b = e2 } --> R(a=e1,b=e2}
{ r with a = e1} --> R(a=e1,b=r.B)
Whether there were one or two attributes (one for 'RecordSyntax' and one for 'CopyAndUpdateSyntax') would be up for discussion. Presumably using either attribute would give result in a declaration-time check that members exist to match constructor arguments.
Matching uppercase properties to lowercase argument names is somewhat inelegant but in the balance is likely to be a reasonable price to pay for following .NET and F# design norms.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663704)**


## Comments ##


#### Comment by Richard Minerich on 3/21/2014 4:53:00 PM ####
As you know, I've certainly been bitten by this before. The other option would be to extend the record syntax a bit so that they can do most of the same things classes can already do.


#### Comment by Will Smith on 3/21/2014 6:10:00 PM ####
If it can be extended or tweaked a little, this would be useful for structs as well. I'm currently having to do this: https://github.com/TIHan/FQuake3/blob/f6ad8a5809db7d57961a55ffd93e1ba0de85dde7/lib/FQuake3.Utils/src/FQuake3.Utils/math.fs#L117 to get a similar effect. Though, there are more than one possible constructors, which may throw a wrench in this...


#### Comment by Jon Harrop on 3/26/2014 5:24:00 AM ####
FWIW, OCaml has functional object update.
@WillSmith: Looking at your code I'm thinking you would want the ability to mark a record type as struct.


#### Comment by Will Smith on 3/26/2014 10:11:00 AM ####
Jon,
I guess that is pretty much what I would want.
Though, I am wondering how multiple constructors would work though in regards to using the record syntax.


#### Comment by Don Syme on 2/3/2016 1:16:00 PM ####
See also /archive/suggestion-6124011-easier-to-copy-data-between-records-of-different-t#comments


#### Comment by Don Syme on 2/3/2016 1:16:00 PM ####
C# is looking into allowing "with" on the proposed C# record types. What ever we do here would best align with that.

