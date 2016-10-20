# Stronger type directed conversion from functions to .Net delegates [5823074] #

**Submitted by Christoph Rüegg on 4/23/2014 12:00:00 AM**  
**25 votes on UserVoice prior to migration**  

It seems in some cases type directed conversion from functions to .Net Func<_,_> delegates only works if the called method has overloads. It would be convenient if it worked the same way for methods without overloads as well.
For example:
open System.Linq
let even n = n % 2 = 0
let seqA = seq { 0..2..10 }
seqA.Where(even) // works
seqA.All(even) // does not work
http://stackoverflow.com/questions/23256355/passing-f-function-to-ienumerable-where-vs-ienumerable-all
http://stackoverflow.com/questions/12933366/f-func-type-inference-difference-between-seq-and-pseq-todictionary



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5823074)**


## Comments ##


#### Comment by Christoph Rüegg on 4/23/2014 6:01:00 PM ####
Workarounds:
seqA.All(System.Func<_,_>(even))
seqA.All(fun x -> even x)


#### Comment by Albert-Jan on 8/1/2014 1:06:00 PM ####
This does work:
even |> seqA.all


#### Comment by Daniel Ferreira Monteiro Alves on 4/26/2015 1:31:00 PM ####
Why not use the .NET native Action and Func and other delegates unstead of the only F# specific closure? Or at least, allow some implicit convertion here.

