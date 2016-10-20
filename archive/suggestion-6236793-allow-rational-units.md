# Allow rational units [6236793] #

**Submitted by Johann Dirry on 7/31/2014 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

In physics and electronics, units with rational exponents are very common, specially in the CGS system. Using it is more natural and makes many formulas easier and the computations more efficient.
Further, rational exponents are also unavoidable without changing the unit system. They are less common in the SI system, but ie. quantities with units like Watts^1/2 are common in electrical engineering.



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

Completed for F# 4.0, see https://visualfsharp.codeplex.com/SourceControl/network/forks/andrewjkennedy/fsharpcontrib/contribution/7632.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6236793)**


## Comments ##


#### Comment by Andrew Kennedy on 10/17/2014 8:08:00 AM ####
A number of people have suggested this. I'm currently prototyping the feature. Couple of design points
* Syntax. Do we permit omission of parentheses e.g. float<kg^1/2> rather than float<kg^(1/2)>. We must disambiguate float<m^2/s> - this is possible, as we didn't previously expect an integer literal after the /. But is it desirable?
* Genericity. "Simplified form" for type schemes is different now e.g. float<'u^2> -> float<'u^2> is equivalent to equivalent to float<'u> -> float<'u> indeed even to float<'u^(1/2)> -> float<'u^(1/2)>.
By the way, I would be interested in any good references to *essential* use of fractional exponents in units.
Andrew.

