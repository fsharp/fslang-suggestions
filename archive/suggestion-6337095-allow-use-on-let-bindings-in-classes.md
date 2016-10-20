# Allow use on let bindings in classes [6337095] #

**Submitted by Mårten Rånge on 8/23/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

A common task in .NET is to implement is IDisposable.
I find the most common task is implementing IDisposable on a class that have fields that are subclasses of IDisposable and no unmanaged resources.
Implementing IDisposable is tedious and error prone. F# supports use on local bindings. Why not support it for member bindings as well?



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Thanks for the suggestion. it’s definitely an interesting one and it took me a long time to decline it. I’ve listed the reasons below. It is possible we might reconsider this at some point, but for now marking it declined as I don’t think we can proceed with it in the language as things stand
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6337095)**


## Comments ##


#### Comment by Mårten Rånge on 8/23/2014 5:12:00 PM ####
The title should read: Allow use on member bindings.
Not sure if I can update it.


#### Comment by Fraser Waters on 8/24/2014 8:16:00 AM ####
There's different ways of implementing IDisposable, it's not immediately clear what use on a member binding would do.


#### Comment by Kevin Ransom on 8/28/2014 12:23:00 PM ####
initial PR with a prototype implementation can be found here: https://visualfsharp.codeplex.com/SourceControl/network/forks/marten_range/visualfsharp/contribution/7318


#### Comment by Don Syme on 2/10/2016 10:56:00 AM ####
After consideration my belief is that this is too hard for F#, because of the reasons discussed in the PRs below: implementing disposal is best done explicitly. Also, when you consider things like the IAsyncDisposable pattern then I don't think it's necessarily the right thing to continue to hardwire F# as a language to the very imperative Dispose pattern.

