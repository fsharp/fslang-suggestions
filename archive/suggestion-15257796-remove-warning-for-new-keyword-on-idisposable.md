# Remove warning for new keyword on IDisposable [15257796] #

**Submitted by Isaac Abraham on 7/18/2016 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

The only time I ever use the new keyword is on Disposables, and even then only to silence the compiler warnings. I'm not sure what purpose the warning serves either, because you can still forget to bind the disposable with the use keyword instead of with let. What's more annoying is that it prevents you from effective pipelining.
Could this be removed from the next F# release, or perhaps replaced with a warning if you bind a Disposable with let instead of use?



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15257796)**


## Comments ##


#### Comment by Alexei Odeychuk on 7/18/2016 6:44:00 AM ####
I support Isaac Abraham's suggestion!


#### Comment by Reed Copsey, Jr. on 7/18/2016 1:31:00 PM ####
Binding a disposable with let is a common requirement if you're authoring libraries.
I find the current warning _very_ valuable. If you never use "new", the warning effectively tells you whenever you allocate something that's disposable, and also provides a simple way in your code to see all uses of disposable.


#### Comment by Gauthier Segay on 7/19/2016 6:00:00 PM ####
I agree with Reed and use same convention, and I do benefit from the warning.
To workaround the fact you can't use the constructor as first class function only takes a single line function while having the warning and convention of using new only for IDisposable could form a nice convention in F# codebases.


#### Comment by Reed Copsey, Jr. on 7/28/2016 7:20:00 PM ####
I just posted an alternative: /archive/suggestion-15448122-add-a-warning-for-new-keyword-used-on-types-which


#### Comment by Jared Hester on 8/11/2016 9:24:00 PM ####
I also find this warning very useful and it definitely should not be removed. Reed's alternative is a much more useful approach.
If you forget to bind to `use` with the `new` right there, that's on you ;P
If the real issue is with how it currently can't be pipelined, why not ask for just that instead?


#### Comment by miegir on 8/15/2016 4:44:00 PM ####
I agree that this warning can be removed and replaced by the warning that IDisposable object should be either bound using 'use' or returned. And that warning should also be reported on methods that return IDisposable values. And, for completeness, using of the 'new' keyword will suppress that new warning, allowing developer to say 'I know that I do here'.

