# Make FSharp.Core collection functions for List, Array and Seq more regular [5663997] #

**Submitted by Don Syme on 3/21/2014 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

F# 3.x is a little irregular in the functions it provides w.r.t. List, Array and Seq. For example, there is no List.groupBy.
Lincoln Atkinson has done an excellent analysis of what’s needed to make this more regular.
The full proposal is available here:
https://github.com/dsyme/FSLangDesignGists/blob/master/CoreLibraryFunctions.md
You can submit comments below or as a pull request to the above file (log in to github and edit directly, your changes will be turned into a pull request by GitHub)



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

This is approved for F# 4.0+
The work has been divided into multiple pull requests which have all been now submitted, reviewed and committed to the “fsharp4” branch, see the overall status and history at https://visualfsharp.codeplex.com/wikipage?title=Status


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663997)**


## Comments ##


#### Comment by Gustavo Guerra on 3/21/2014 11:35:00 AM ####
Related to this, would be good to have something like LazyList in the standard collection, as seq doesn't support pattern matching


#### Comment by Jon Harrop on 3/21/2014 12:01:00 PM ####
This is somewhat nice but potentially very bad. I think it is much more important to get the full complement of functions in each of the List, Array, Set and Map modules that actually leverage the specific benefits of those data structures.
For example, Set.partition should not be there because it is linear in time when we could have a log time Set.split function like OCaml. Furthermore, users cannot even add efficient log-time functions like Set.split because the data structure is abstract. The Map module should have functions equivalent to union, intersection and difference and a sub function that accepts a set of keys. I would value these much more highly than, for example, a List.singleton function when we already have the list literal syntax [x] or an Array.take function when we already have the array slice syntax xs.[0..n-1].


#### Comment by Don Syme on 3/21/2014 12:28:00 PM ####
Gustavo - Please add separate entries for separate requests
Jon - Likewise, yours is a separate request for a Set.partitionAt, and other functions over Map. They should be bundled into a single separate request.


#### Comment by Don Syme on 3/21/2014 12:30:00 PM ####
I've updated the title to reflect the proposal more specifically.


#### Comment by Richard Minerich on 3/21/2014 4:43:00 PM ####
Hrm, I don't think breaking changes to F# Core would be a good thing at all. It would only go to show those companies already using F# that we can't be trusted.
Adding more functionality would certainly be useful though!


#### Comment by Patrick Q on 3/23/2014 8:19:00 PM ####
Always wanted this and wondered why Seq had a groupBy but not List. It's such a pain, not to mention inefficient, to be given a list and than have to use Seq for some operation only to convert it back to a list again!


#### Comment by Don Syme on 6/25/2014 9:39:00 AM ####
@Jon - note that one aspect of the proposal here is regularity. Looking at the matrix in the design-document link above, it is hard to justify leaving any particular entry in the top table unimplemented.
@Rick - there is no proposal to make a breaking change to FSharp.Core.


#### Comment by Robert Jeppesen on 6/29/2014 5:39:00 PM ####
Most of the suggestions are fine, but it doesn't make sense to me to add something like Seq.scanBack or Seq.reduceBack. Seems to me the library is suggesting that Seq is a fine choice for doing these things.


#### Comment by Robert Jeppesen on 6/29/2014 5:47:00 PM ####
To further elaborate, List is also a poor choice for scanBack, but it's worse for Seq, cause with Seq, the assumption that a seq will never be materialized in memory at once is violated.


#### Comment by Fraser Waters on 7/8/2014 8:20:00 AM ####
Not sure if this should be added as a new suggestion or if it fits ok here. While it's nice that List is getting Last can we have a method to get all but the last element as well (It's called init in Haskell but that's already taken). That would give us:
Head - First element
Last - Last element
Tail - All but first
Init/Front/? - All but last
Which has a nice symmetry to it.


#### Comment by Mariusz on 7/30/2014 2:59:00 PM ####
I think that simple count function that takes predicate function and collection and returns number of item that satisfy the predicate is missing.
For me as a C# developer who has Count function in LINQ (http://msdn.microsoft.com/en-us/library/vstudio/bb535181%28v=vs.100%29.aspx) it's kind of weird that this function is missing.
I know that I can use fold function but still dedicated count function will be much more concise and readable.


#### Comment by Nick on 9/12/2014 2:03:00 AM ####
@Mariusz
Is that the same as the Length function?


#### Comment by Don Syme on 9/12/2014 6:27:00 AM ####
@Nick @MariusZ I've started a discussion about a potential "countWhere" function here: https://github.com/fsharp/FSharpLangDesign/issues/36

