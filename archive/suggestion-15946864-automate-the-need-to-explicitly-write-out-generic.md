# Automate the need to explicitly write out generic parameter constraints in classes [15946864] #

**Submitted by Marko Grdinic on 9/6/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Given that F# already automatically tells you what member constraints the classes should have, why not go an extra step and have the compiler write them out implicitly like in normal let statements.
I just recently had a situation where in a class I had to explicitly write a bunch of them all out like in the following:
```
type FFRec<'state when 'state: (member Tape: Stack<unit -> unit>)
and 'state: (member Mem: ObjectPool)
and 'state: (member Str: CudaStream)
and 'state: (member Workspace: Workspace)
and 'state: (member IsInferenceOnly: bool)> =
```
This would be bad if I had a bunch of classes where for each one, I had to write out every constraint.
Of course I replaced the above with a single subtyping constraint, but is there any reason why the compiler could not have done this automatically? Also if that is not possible, would it be possible to introduce an abbreviation feature for type constraints instead of just types. They would make structural typing a lot more palatable.
Having recently been introduced to structural typing in F#, I am quite a fan of it and even the syntax which bothered me at the beginning does not look worse than anything you might find in Scala for example. I think this particular feature of the language could be a great selling point if it was made nicer.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15946864)**


## Comments ##

