# Add a tryUnbox, isNull builtin operators [6099437] #

**Submitted by Dave Thomas on 6/25/2014 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

Add builtin functions:
tryUnbox : obj -> 'T option
isNull: 'T -> bool when 'T : null
The first is an unbox operation which if successful would return Some<'a> on a successful unbox and None for a fail. This would allow the Option module to be used efficiently for single type matches and processing.



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

Completed for F# 4.0, see https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7672
Don Syme, F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6099437)**


## Comments ##


#### Comment by Don Syme on 6/25/2014 4:22:00 PM ####
How about the operator has the name "tryUnbox" , as in x |> tryUnbox<string>


#### Comment by Dave Thomas on 6/25/2014 4:32:00 PM ####
I was thinking more of an extended operator to supplement :> and :?>
Nothing spring to mind that would be intuitive though.


#### Comment by Dave Thomas on 6/26/2014 3:05:00 AM ####
Essentially its just:
let inline tryUnbox<'a> (x:obj) =
match x with
| :? 'a as result -> Some (result)
| _ -> None
Although it might want some direct IL generated like the other primitives.


#### Comment by Anonymous on 6/27/2014 10:40:00 PM ####
Looks great. How about ':/>'
?
Keystrokes are almost the same, just one less 'Shift' keypress.


#### Comment by Dave Thomas on 7/2/2014 4:34:00 AM ####
This is really similar to: /archive/suggestion-6103054-add-option-ofnull-to-help-remove-nulls
I would prefer this as a primitive though.
Don would a symbol be considered here?


#### Comment by Don Syme on 7/2/2014 7:46:00 AM ####
Hi Dave,
My instinct is that we wouldn't consider a symbol here, but would consider a named primitive ala tryUnbox
cheers
don


#### Comment by Dave Thomas on 7/6/2014 3:41:00 AM ####
I think a named function would suffice as this can be piped into in any case.
I expect a more efficient implementation could be achieved through use of in line IL e.g. (# ... # )


#### Comment by Don Syme on 11/10/2014 11:28:00 AM ####
I have submitted a PR for tryUnbox and isNull in FSharp.Core for F# 4.0+ https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7672

