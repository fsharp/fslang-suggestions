# Bottom type [6586873] #

**Submitted by Janek Paw on 10/20/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Bottom type
Bottom type for all types. Allows you to implement usefull functions like unimplemented (see scala ???)



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Thanks for the suggestion. Declined per my comment below.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6586873)**


## Comments ##


#### Comment by exercitus vir on 10/22/2014 3:57:00 AM ####
This is definitely better than e.g. failwith, which returns an 'a instead of a bottom type, which would be more appropriate.


#### Comment by Kai Noda on 10/28/2014 8:29:00 PM ####
We may introduce a new [<NoReturn>] attribute, borrowed from GCC, and mark functions such as Environment.Exit with it.
Cf. https://gcc.gnu.org/onlinedocs/gcc/Function-Attributes.html


#### Comment by Greg Chapman on 11/15/2014 11:02:00 AM ####
I'm not really familiar with Scala, but I like what I understand of the ??? construct, so lately I've been using this in F#:
[<GeneralizableValue>]
let TODO<'a> : 'a = raise (NotImplementedException())
which lets me write TODO whereever I'm not ready to supply an implementation. Would a bottom type provide benefit beyond this?


#### Comment by Don Syme on 2/4/2016 6:08:00 PM ####
We considered this for F# 1.0 but decided to stick to the OCaml way of just using a type variable. We won't revisit that decision at this point

