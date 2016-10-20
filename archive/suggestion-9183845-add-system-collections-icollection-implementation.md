# Add System.Collections.ICollection implementations to F# list/set/map [9183845] #

**Submitted by Eirik George Tsarpalis on 8/5/2015 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

ICollection is a useful interface that inherits IEnumerable. Inputs implementing ICollection are utilized by libraries such as LINQ, Nessos.Streams and MBrace in order to optimize partitioning of data. Curiously, none of the F# collections (list/set/map) implement ICollection (however the latter two do implement ICollection<T>, which is a different interface designed for mutable collections). It is currently impossible to extract the length/count of a boxed list/map without performing some sort of reflection, which is not always desirable.
I suggest that future versions of F# core implement this.
See also https://github.com/Microsoft/visualfsharp/issues/570#issuecomment-128000307



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Approved in principle, see my comment below
We will open an RFC for this in due course.
https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9183845)**


## Comments ##


#### Comment by Lincoln Atkinson on 8/5/2015 11:55:00 AM ####
In order to accurately track the length of a list, an additional length field would need to be added to every node. That would be a not insignificant increase the size of lists.
Also worth noting that the F# runtime is allowed to cheat and mutate lists in the name of performant front-to-back list creation. If length needs to be tracked, some of these implementations will be required to perform a second pass to update the length fields (e.g. List.filter, which builds result list front to back but has no way to know final length ahead of time)


#### Comment by Lincoln Atkinson on 8/5/2015 12:07:00 PM ####
So while I agree 100% that fast access to .Length would be very useful in a number of situations, it would come at the price of memory and CPU for all users, all the time. That's not to be taken lightly.
And in fairness I must also note that some runtime APIs would in fact benefit from this - e.g. List.length (obviously), List.nth/List.take/List.skip (can detect 'index out of range' type errors cheaply).


#### Comment by Eirik George Tsarpalis on 8/6/2015 4:03:00 AM ####
Good point.
My thinking in this case was not to make .Length a constant time operation, but rather expose the current .Length implementation for untyped access. Perhaps the ICollection.Count property comes with the implicit assumption that it should be constant time, however in practice the performance of .Length is acceptable and in fact much, much better than running Seq.length.
My motivation behind this feature request is the following: when writing libraries that consume user-supplied IEnumerables (such as PLINQ) it is often good practice to specialize on the input type. This is particularly true in the case in the case of parallel/distributed computation where proper partitioning of input data is important. If I were to write a partitioning function that accepts IEnumerable<T>, handling lists is no problem (given that my library is F# aware):
```
let partition (n : int) (ts : seq<'T>) =
match ts with
| :? 'T [] as ts -> partitionArray n ts
| :? ('T list) as ts -> partitionList n ts
| :? ICollection<'T> as c -> partitionCollection n c
(* add more cases here *)
| _ -> partitionSeq n c // slowest, most naive approach
```
If I were to write the same partitioning function for IEnumerable, my options become more limited
```
let partition (n : int) (e : IEnumerable) =
match e with
| :? System.Array as a -> partitionArray n a
| :? ICollection as c -> partitionCollection n c
| _ ->
// no longer possible to identify lists, need to rely on clunky reflection
let t = e.GetType()
if t.IsGenericType && t.GetGenericTypeDefinition() = typedefof<_ list> then
// etc etc
```


#### Comment by Paul Westcott on 8/7/2015 4:57:00 AM ####
I always think of properties as O(1) operations. ICollection.Count should thus remain as as O(1) operation. If you want untyped access like it then a sperate interface like IFSharpList should be created that implements Length or named like a function Count() as per the IEnumerable<> extension. (Maybe it could implement other functionality as well; maybe IsEmpty; GetElementtType; maybe it derives from IEnumerable... Maybe I'm just clutching at straws!)


#### Comment by Don Syme on 2/4/2016 4:43:00 PM ####
Re this:
> Also worth noting that the F# runtime is allowed to cheat and mutate lists ...
FSharp.Core does this but only before list objects escape back to user code. (in any case it's not relevant to the issue under discussion here, just mentioning this in case people were wondering)


#### Comment by Don Syme on 2/5/2016 9:18:00 AM ####
In balance I think this is a reasonable suggestion and will mark it approved-in-principle
Alternatively we could implement IReadOnlyCollection https://msdn.microsoft.com/en-us/library/hh881542(v=vs.110).aspx now that FSharp.Core 4.4.0.0+ target .NET 4.5 and .NET 4.0 is old history.


#### Comment by Marc Sigrist on 2/10/2016 4:55:00 AM ####
FWIW, I have worked in several larger F#-to-C# projects, and I have used IReadOnlyCollection extensively. So I think implementing IReadOnlyCollection would be a great idea.

