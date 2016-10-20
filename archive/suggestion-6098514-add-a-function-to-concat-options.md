# Add a function to concat Options [6098514] #

**Submitted by Huw Simpson on 6/25/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I suggest the following enhancement to the Option module:
// Combines the given option-of-option into a single option.
let concat value =
match value with
| None -> None
| Some o -> o
concat : value : 'a option option -> 'a option



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

Declining as “Option.bind id” is a suitable workaround, or it is very easy to define this function in user code.
Don Syme Current BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6098514)**


## Comments ##


#### Comment by Daniel Fabian on 6/25/2014 2:11:00 PM ####
You can use "Option.bind id" for that exactly


#### Comment by exercitus vir on 7/8/2014 5:59:00 AM ####
I would call that "flatten" instead. concat would take more than one (unnested) option.

