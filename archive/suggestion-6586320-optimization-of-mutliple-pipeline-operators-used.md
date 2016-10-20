# Optimization of mutliple pipeline operators used in single statement [6586320] #

**Submitted by Bartosz Sypytkowski on 10/20/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Using an example:
```fsharp
let f x y z = ...
let fn = f <| 1 <| 2
```
Second line will result with generation of IL code for intermediate classes and delegates for each `<|` operator used in this single statement. Desired behavior would be to optimize this code to equivalent of `let fn = f 1 2`, that means all following pipeline intermediate results should be aggregated into single one containing all applied partial function applications.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

As per comment, please just submit a PR directly to the http://github.com/Microsoft/visualfsharp repository.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6586320)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 2:01:00 PM ####
I think a PR for this could just be submitted directly to the http://github.com/Microsoft/visualfsharp repository. It doesn't need to be tracked here as a language design item.

