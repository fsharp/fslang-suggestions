# String Interpolation [5678806] #

**Submitted by Liviu on 3/25/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

It will be excellent to have string interpolation with intellisense support as opposed to the anacronical printf variants.
Syntax may be:
let a = 40
let p = "John"
let b = $" ${p} has $(a*2) items"



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

Declining as /archive/suggestion-6002107-steal-nice-println-syntax-from-swift is close enough to act as a “duplicate”.
Don Syme, F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5678806)**


## Comments ##


#### Comment by Liviu on 3/25/2014 12:50:00 PM ####
correction:
let b = $" $(p) has $(a*2) items"


#### Comment by Mauricio Scheffer on 3/27/2014 10:51:00 AM ####
-1 to this. I agree with Martin Odersky's argument in http://permalink.gmane.org/gmane.comp.lang.scala.debate/872 , this doesn't really save much typing. (even though Scala ended up getting string interpolation after that discussion).
Plus it's really easy to forget the interpolation symbol '$', and then you end up with the literal string "${p} has $(a*2) items", this has happened to me many times while programming in Scala.
Alternatively, one could implement this as a type provider, which isn't as terse but it's explicit about the variables being passed and could do strict type checking.


#### Comment by Vasily Kirichenko on 3/27/2014 11:58:00 AM ####
I'm also -1 for this as it cannot be partially applied.


#### Comment by Mauricio Scheffer on 6/2/2014 6:18:00 PM ####
Similar suggestion but restricted to printf only /archive/suggestion-6002107-steal-nice-println-syntax-from-swift

