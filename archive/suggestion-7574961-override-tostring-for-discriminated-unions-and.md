# Override `ToString` for discriminated unions and records [7574961] #

**Submitted by Vasily Kirichenko on 4/15/2015 12:00:00 AM**  
**181 votes on UserVoice prior to migration**  

It's a pain and dirty to add `override x.ToString() = sprintf "%A" x` to every type in order to make `String.Format()` happy:
type T1 =
{ Id: int
Version: string }
override x.ToString() = sprintf "%A" x
type DU =
| C1 of int
| C2
override x.ToString() = sprintf "%A" x
I think it's very easy to teach the compiler generate this override automatically for all user types.



## Response ##
** by fslang-admin on 6/23/2016 12:00:00 AM **

Marking as planned, though we need to work out the details
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7574961)**


## Comments ##


#### Comment by Steffen Forkmann on 4/15/2015 3:38:00 AM ####
This is a real world issue and a problem in projects like paket or https://github.com/adamchester/EaToSql/blob/master/src/EaToSql/Model.fs


#### Comment by Steffen Forkmann on 4/15/2015 3:44:00 AM ####
Also it's hard to debug such types without the automatic tostring implementation. Debugger just shows the type name.


#### Comment by Matthew Peacock on 4/21/2015 6:21:00 PM ####
However, %A is very very slow, ideally the implementation should not do any reflection at runtime, but be based on code generated at compile time.


#### Comment by exercitus vir on 6/19/2015 6:00:00 PM ####
I am against this. ToString() carries no semantics. To what kind of string? Is it an atomic value or structured value? Is it for logging or display to the user? There is no consistency. The ToString() method should simply be deprecated.
You can always simply call sprintf "%A" any structural type to get a good structured representation even if its very slow.

