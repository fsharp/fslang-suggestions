# allow use to not bind the expression to a name [12838449] #

**Submitted by Gauthier Segay on 3/7/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

In C#, one can use using(CreateSomeDisposable()) without binding the expression to a name.
Same construct in F# is not allowed, forcing a workaround such as
use __ = CreateSomeDisposable()
allow to make it like this:
use CreateSomeDisposable()



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12838449)**


## Comments ##


#### Comment by lr on 10/6/2016 1:22:00 PM ####
In my opinion the bigger annoyance is that a use expression can't even be bound to _ (single underscore), so if I want to use multiple uses, I need to write something like
use _1 = CreateSomeDisposable()
use _2 = CreateSomeDisposable()
If I could instead bind it to the wildcard character _, then I would be happy:
use _ = CreateSomeDisposable()
use _ = CreateSomeDisposable()

