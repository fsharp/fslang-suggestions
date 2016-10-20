# Add support for symbolic stacktraces in computation expressions [13499082] #

**Submitted by Eirik George Tsarpalis on 4/20/2016 12:00:00 AM**  
**59 votes on UserVoice prior to migration**  

One of the biggest problem in async or computation expressions in general is lack of proper stacktraces when exceptions are raised. This is a major annoyance when debugging in the large, often leading to errors whose origin cannot be traced.
I recently made a blog post arguing for the addition of language features that would make symbolic stacktraces possible for computation expression authors: https://eiriktsarpalis.wordpress.com/2015/12/27/reconciling-stacktraces-with-computation-expressions/
Symbolic stacktraces is a feature that has already appeared in languages like C# (https://github.com/ljw1004/async-exception-stacktrace) and JavaScript (http://www.html5rocks.com/en/tutorials/developertools/async-call-stack/)



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

See Eirik’s comment below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13499082)**


## Comments ##


#### Comment by Eirik George Tsarpalis on 6/13/2016 7:32:00 AM ####
From a compiler perspective, I believe that the issue has been covered by RFC FS-1012..
C.f.
/archive/suggestion-8899330-f-compiler-should-support-callerlinenumber-calle
https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1012-caller-info-attributes.md
https://github.com/Microsoft/visualfsharp/pull/1114

