# add support for dimensions and implicit unit conversions [6236802] #

**Submitted by Johann Dirry on 7/31/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Dimensions could be described as discriminated unions of a set of units (Measure's). It should also be possible to convert units explicitly to the base unit.
// some units
[<Measure>] type Kelvin
[<Measure>] type DegreeCelsius
[<Measure>] type DegreeFahreinheit
// Example: dimensions
// Advantage: failwith condition not needed anymore, because of additional checking by the compiler -> less bugs
[<Measure>] type Time = Second | Minute
[<Measure>] type Temperature = Kelvin | DegreeCelsius | DegreeFahreinheit
let temperatureToSI (value : float<Temperature>) : float<Kelvin> =
match value with
| :? float<Kelvin> -> value
| :? float<DegreeCelsius> -> (value - 273,15<DegreeCelsius>) * 1.0<Kelvin/DegreeCelsius>
| :? float<DegreeFahreinheit> -> (value + 459,67<DegreeFahreinheit>) * 5.0<Kelvin> / 9.0<DegreeFahreinheit>
// | _ -> failwith "unknown temperature"
// Example: implicit unit conversion
// Advantage: derived units always converts to base unit when used
[<Measure>] type Second
[<Measure>] type Minute (value:float) : (float<Second>) = value * 60.0<Second/Minute>



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion. Marking as declined as part of house keeping per my comment below. However we’re still interested in collecting more feedback over time on this issue.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6236802)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 5:42:00 AM ####
We decided against this in F# 2.0 because it requires witness passing (i.e. passing extra arguments around in generic code and storing them in generic classes) , and it is not particularly apparent where the floating point conversions get applied in generic code
I also would have though this issue might get more votes, and it's interesting to me that it has only one.
I will mark the issue as declined as part of house keeping, though we're still interested in collecting more feedback on this

