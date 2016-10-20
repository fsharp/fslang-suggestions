# Normalize Collections API for Array2D Module [7334486] #

**Submitted by Jared Hester on 3/26/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

With the upcoming rollout of the normalized collections API across the List, Array, and Seq modules, it would be great to see Array2D ( and possibly the other higher dimension Array Modules) brought into the fold.
A large portion of the collections API (avg, contains, exists, find, fold, forall, max, min, scan, sum, etc.) could be implemented for Array2D in a way that conforms with the other collections modules.
Other functions like append and concat should be workable if they enforce constraints on the length of the [,]'s dimensions similiar to the ones on the length of collections for the zip functions.
Functions like filter that will likely remove elements in a manner that doesn't map to a filled 'T [,] could return 'T [] instead.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7334486)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 1:55:00 PM ####
Hi Jared
My view is that this best lies outside the core. It would be entirely reasonable to have it in an FSharp.Core.ArrayFunctions community project and nuget package.
Don Syme, F# Language and Core Library Evolution

