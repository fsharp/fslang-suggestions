# Add support for forward piping the result of an async workflow [8151819] #

**Submitted by Wallace Kelly on 5/28/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

The sample code looks much better at https://gist.github.com/WallaceKelly/f146180d5946b2b004bb
When calling an async function within an async workflow, we sometimes end up with code like the following:
let getDataFromServer1() =
async {
let! data = downloadData()
return
data
|> Seq.where isUseful
|> Seq.sortBy sortSelector
|> Seq.toList
}
Notice that we must bind the result to a label and then pipe the result using that label.
If we use Async.RunSynchronously, the syntax is much cleaner. Because Async.RunSynchronously returns the result 'T, we can build a single pipeline, as follows, without having to bind the result to a label:
let getDataFromServer2() =
async {
return
downloadData()
|> Async.RunSynchronously
|> Seq.where isUseful
|> Seq.sortBy sortSelector
|> Seq.toList
}
However, the problem with relying on Async.RunSynchronously is that it can be inefficient. Unlike the solution that uses let!, the calling thread is blocked and not available to do other work.
Some have suggested that Async.map solves this problem. However, Async.map returns an Async<'T>, not a 'T (like Async.RunSynchronously). Using Async.map works, but it too requires cluttering the code with a temporary label:
let getDataFromServer3() =
async {
return!
downloadData()
|> Async.map(fun d ->
d
|> Seq.where isUseful
|> Seq.sortBy sortSelector
|> Seq.toList)
}
What could be a
What we want is the efficiency of let! or Async.map, but the pipeline syntax of Async.RunSynchronously.
There are several options. We could introduce a pipeline-like operator, which works like let!. For example, we could use !>. The code might look like this:
let getDataFromServer4() =
async {
return
downloadData()
!> Seq.where isUseful
|> Seq.sortBy sortSelector
|> Seq.toList
}

The compiler would simply translate the above into the equivalent of getDataFromServer1().
Alternatively, we could add a function that accomplishes the same. We might call it Async.RunAsynchronously. In this case, the code would be:
let getDataFromServer5() =
async {
return
downloadData()
|> Async.RunAsynchronously
|> Seq.where isUseful
|> Seq.sortBy sortSelector
|> Seq.toList
}

Again, the resulting IL would be the same as getDataFromServer1()

In summary, we want something that works like let!, but for forward-piping.



## Response ##
** by fslang-admin on 6/9/2015 12:00:00 AM **

Declined as suggested by the author
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8151819)**


## Comments ##


#### Comment by Wallace Kelly on 5/29/2015 9:50:00 AM ####
I received this suggested operator...
let (|>>) xA x2y = async.Bind (xA, x2y >> async.Return)
...which works very nicely....
async {
return! downloadData()
|>> Seq.where isUseful
|>> Seq.sortBy sortSelector
|>> Seq.toList
}
Based on this, I'm considering deleting this suggestion. Thoughts?

