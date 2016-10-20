# Allow the addition of operators in type extensions, and also operators on internal types [5695277] #

**Submitted by Gustavo Guerra on 3/28/2014 12:00:00 AM**  
**80 votes on UserVoice prior to migration**  

This is currently not allowed:
type Foo with
static member (+) (foo1, foo2) = foo1.Bar + foo2.Bar



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5695277)**


## Comments ##


#### Comment by Mauricio Scheffer on 4/9/2014 10:09:00 PM ####
This seems more concrete than /archive/suggestion-5666323-operator-overloads-problem-in-f but since it can already be done with inline + static type parameters I wonder what would be the benefit of doing it via type extensions.


#### Comment by Don Syme on 6/20/2014 2:04:00 PM ####
See some commentary here that discusses a related problem and the relevant commpiler code: https://visualfsharp.codeplex.com/workitem/2


#### Comment by Anonymous on 8/17/2014 1:09:00 PM ####
This would help with generic arithmetic on novel types, e.g. http://stackoverflow.com/questions/25346246/why-cant-we-satisfy-f-static-member-constraints-with-type-extensions/25347602#25347602


#### Comment by Bryan Edds on 2/25/2015 10:08:00 AM ####
Just ran into this problem today, and worked around it with the scary inline workaround :) Would be nice if this worked and didn't cause any problems elsewhere!


#### Comment by exercitus vir on 6/12/2015 10:32:00 PM ####
Yes, I need this too.

