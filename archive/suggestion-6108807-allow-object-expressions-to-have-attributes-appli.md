# Allow Object expressions to have attributes applied to them [6108807] #

**Submitted by Dave Thomas on 6/27/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

In the simplest case something like this would be possible:
[<MyAttribute>]
let makeResource name =
{ new System.IDisposable
with member this.Dispose() = printfn "%s disposed" name }
And then when the code is compiled the expression thats generated would also have the attribute applied to it.
This would interoperability with frameworks that use declarative attributes which would otherwise require adding a full type



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6108807)**


## Comments ##


#### Comment by Vasily Kirichenko on 6/28/2014 1:44:00 AM ####
I think it's more logical to place attributes right before object expression itself, like this:
let makeResource name =
[<MyAttribute>]
{ new System.IDisposable with
member this.Dispose() = printfn "%s disposed" name }
It's also better since we now can apply attributes not only in bindings, but in any expression:
func ([<MyAttribute>]
{ new System.IDisposable with
member this.Dispose() = printfn "%s disposed" name },
anotherArg)


#### Comment by Don Syme on 7/18/2015 1:28:00 PM ####
I tend to agree that this should be supported (though the location for the attributes would be different to shown above)


#### Comment by zhonglei chen on 1/30/2016 12:29:00 PM ####
I agree with this suggestion due to performance consideration.
If we can add attribute to object expression, we can apply the following pattern to improve the performance of algorithms:
let sort<'a, 'c when 'c :> System.Collection.Generic.IComparer<'a>>( array : 'a[], comparer : 'c ) = ...
let filter<'a, 'p when 'p :> XXX.Predicate<'a>>( array : seq<'a> , predicate : 'p) = ...
...
now, users can access these algorithms by passing an object expression:
sort([0..1000000], { new IComparer<int> with member this.Compare(a, b) = a.CompareTo(b) })
filter([0..1000000], { new Predicate with member this.Filter(a) = a % 2 = 0 })
at this point, it looks like the client code injection mechanism goes back to java, so how can we benifit from this ?
we can apply the struct attribute to object expression to force the anonymous type to be generated as struct:
sort([0..1000000], [<Struct>] { new IComparer<int> with member this.Compare(a, b) = a.CompareTo(b) })
filter([0..1000000], [<Struct>] { new Predicate with member this.Filter(a) = a % 2 = 0 })
and then the JIT compiler will generate some individual algorithms for each anonymous type here, and inlining the Compare/Filter method into inner loop of algorithm.
we can benifit much from this.

