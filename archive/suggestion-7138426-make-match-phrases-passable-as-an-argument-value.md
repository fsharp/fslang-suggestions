# make match phrases passable as an argument value [7138426] #

**Submitted by Steven Taylor on 2/24/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

when walking tree DU structures, it would be useful to pass match expressions to a walking function instead of being forced to hardwire it. Perhaps this also requires a match signature.
e.g.
static member walk ast =
let rec walk ast = ast |> function | ListOfX(_,l) -> [for e in l -> walk e] |> List.concat | e -> [e]
walk ast



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7138426)**


## Comments ##


#### Comment by Fraser Waters on 2/26/2015 5:51:00 AM ####
You can already do this, match functions can be passed as lambdas.


#### Comment by Don Syme on 6/9/2015 2:07:00 PM ####
Yes, this is what "function" is for as far as I understand the request.

