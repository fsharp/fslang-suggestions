# add isNotNull to FSharp.Core [13419354] #

**Submitted by Gauthier Segay on 4/13/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

Using "not (isNull a)" in conditions forces usage of parens or pipe operator and is not optimal readability compared to "a |> isNotNull" or "isNotNull a"
let inline isNotNull a = not (isNull a)
in absence of this function, people often take the shortcut of "a <> null" which according to lint is not optimal.



## Response ##
** by fslang-admin on 6/13/2016 12:00:00 AM **

Declining per my comment below.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13419354)**


## Comments ##


#### Comment by Martin Schinz on 4/18/2016 2:48:00 AM ####
Why not Option.fromNullable and check isNone?


#### Comment by Vasily Kirichenko on 4/18/2016 3:30:00 AM ####
@Martin because it would cause an unnecessary memory allocation (in case it returns Some)
I don't see why notNull was added. I strongly believe `=` operator should be fixed instead.


#### Comment by Carl Patenaude Poulin on 4/19/2016 12:02:00 PM ####
I just do (not << isNull)...


#### Comment by Don Syme on 6/13/2016 5:28:00 AM ####
The design principle here is that we don't add negations of operators in FSharp.Core. For example we don't add ``List.notContains`` or ``map.Doesn'tContainKey``. We just have to write ``not (List.contains x l`` or ``x |> List.contains x |> not``
I think it's best that we don't start making individual exceptions to this rule.


#### Comment by Daniel Robinson on 9/13/2016 9:08:00 AM ####
Did I miss something? It looks like this was added to FSharp.Core -
https://github.com/Microsoft/visualfsharp/blob/36050db52bc4d4876b16b7f62b5e67cdee34f2aa/src/fsharp/FSharp.Core/prim-types.fsi#L2157-L2158


#### Comment by Gauthier Segay on 9/13/2016 12:53:00 PM ####
Daniel, you are right, it was added recently because, I guess, it is useful even in the compiler itself (to replace non optimal comparison operators).

