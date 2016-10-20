# Early return from functions [5688699] #

**Submitted by Braden Evans on 3/27/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

I have found that when porting code from other languages (especially optimized loopy code) the lack of early return is a real pain point. It is always possible to re-arrange code (especially with pattern matching) but it can be very time consuming and the "gist" of many algorithms can be lost.
I don't think this is a desirable feature for general use, perhaps this could be made just ugly enough to discourage abuse - maybe require an attribute on functions that use it?
I'm sure this will be highly controversial, my own experience is that imperative code in f# is still nicer than other languages, and I would like to be able to write everything in f# instead of splitting between f# and c#.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per my comment
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5688699)**


## Comments ##


#### Comment by Gustavo Guerra on 3/28/2014 9:54:00 AM ####
If you really need that you can use http://tomasp.net/blog/imperative-i-return.aspx/
I think it's a bad idea to have in the language


#### Comment by Patrick Q on 3/31/2014 6:23:00 AM ####
Early returns is a bad idea that definitely should NOT be introduced. Simulating early returns should be done via computation expressions.


#### Comment by Will Smith on 3/31/2014 1:34:00 PM ####
Agree with the previous comments. Returns should not be introduced, encourages bad styles.


#### Comment by Isaac Abraham on 4/4/2014 4:24:00 PM ####
In C# I very much like early returns rather than the usual practice of "declare a variable called ReturnValue at the start of the method, assign it in various random places throughout the method, and then return whatever it is at the end". However, in F# I find that it's usually not necessary as expressions, pattern matching and the ability to declare arbitrary functions inline of one another means that you can still easily reason about code and have only one return point.


#### Comment by Don Syme on 2/3/2016 3:08:00 PM ####
I'm inclined to decline this: F# is expression oriented and that is one of its strengths. Early returns become a little harder, but the advantages of being expression oriented outweigh the problems it brings

