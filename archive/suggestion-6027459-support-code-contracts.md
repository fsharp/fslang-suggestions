# Support code contracts [6027459] #

**Submitted by Onur on 6/9/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Currently Code Contracts doesn't work in F# properly, especially in the primary contructors. Although F# is null safe and functional , I still find code contracts for the public surface of the projects.



## Response ##
** by fslang-admin on 6/20/2014 12:00:00 AM **

I’m supportive of this if we can identify what’s needed.
Please provide more details about what would need to change with F# to make code contracts work, and reopen a new suggestion for each necessary change.
Thanks
Don


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6027459)**


## Comments ##


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 6/10/2014 3:00:00 AM ####
I have run out of votes but +3 for this


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 6/20/2014 9:10:00 AM ####
This is surely a request for the Code Contracts feature team at Microsoft. What needs to change for F# to make this work?
thanks
Don Syme, BDFL for F# Language


#### Comment by Onur on 6/20/2014 9:21:00 AM ####
Don,
Code Contracts are almost working with F# as in C# (besides IDE support) except one thing. The F# constructors. If we put Contract.Requires inside a constructor, then Code Contracts complains this/me cannot be used inside a constructor regerdless of primary or secondary ctor. Maybe this is all code contracts fault. I just wish someone from F# team contacted to Code Contracts for a resolution or vice versa


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 6/20/2014 10:30:00 AM ####
Have a look at WhyML (link on http://why3.lri.fr/) as ML is very much close to F#.


#### Comment by Onur on 11/3/2014 8:48:00 AM ####
Don, F# compiler does a lot of magic. Especially if we put Contract.Requires to the beginning of a method or a constructor, F# can (if it is a constructor it will) put additional code.
There is nothing code contract team can do anything about this because this is about how F# compiler works. It basically adds code to the prologue methods and ctors. What compiler can do is to respect System.Diagnostics.Contract class and don't put any code above it.

