# Make Option Types implement IEnumerable<'T> [5665274] #

**Submitted by Richard Minerich on 3/21/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

It's such a pain to need to manually change option types into seqs when they're already obviously perfectly fit for being a collection. It sure would be nice to just be able to collect them up, or use them with "yield!".



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

As indicated in the comments, this can’t be done because of the use of “null” as a representation for “None”.
Don Syme, BDFL Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5665274)**


## Comments ##


#### Comment by Jon Harrop on 3/27/2014 5:28:00 AM ####
Problem is None is represented as null internally so enumerating None would give a null reference exception.


#### Comment by Richard Gibson on 3/27/2014 11:52:00 AM ####
There doesn't seem to be anything wrong with this: open System.Collections
type MyOption<'t> =
| Some of 't
| None
interface seq<'t> with
member this.GetEnumerator() =
(seq {
match this with
| Some t -> yield t
| None -> ()
}).GetEnumerator()
interface IEnumerable with
member this.GetEnumerator() =
(this :> IEnumerable).GetEnumerator()

None |> Seq.iter (printfn "%s")


#### Comment by Richard Gibson on 3/27/2014 11:53:00 AM ####
The same goes for Ref; you could argue that a reference cell of 'T is a sequence of 'T with exactly one item in it.


#### Comment by Richard Gibson on 3/27/2014 12:01:00 PM ####
In fact, there may be a way for any generic union type to implement seq... Take a look at this Tree implementation:
open System.Collections
type Tree<'t> =
| Branch of 't Tree * 't Tree
| Leaf of 't
interface seq<'t> with
member this.GetEnumerator() =
(seq {
match this with
| Branch (left, right) ->
yield! left
yield! right
| Leaf data -> yield data
}).GetEnumerator()
interface IEnumerable with
member this.GetEnumerator() =
(this :> IEnumerable).GetEnumerator()

Branch(Branch((Leaf "two"), Leaf "three"), Leaf "one") |> Seq.iter (printfn "%s")


#### Comment by Richard Minerich on 6/20/2014 12:09:00 PM ####
It's too bad we don't have extension interfaces, as you can do a null check in extension methods.

