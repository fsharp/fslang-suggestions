# Allow basic integer numeric type names in a for loop (from Ada 2012) [12564057] #

**Submitted by Alexei Odeychuk on 3/2/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

I suggest using basic integer numeric type names (namely, sbyte, byte, int16, uint16, int (int32), uint32, int64, uint64) in a for loop meaning to try every value of the type (from Ada 2012).
For example,
let ourSequence = seq { for i in int -> i } // ourSequence : seq<int>
let ourList = [ for i in byte -> i ] // ourList : byte list
for i in sbyte do printf "%A" i
I think it's a good idea to allow basic integer numeric type names in for loops just as in Ada 2012 and treat such types by the F# compiler as types compatible with IEnumerable and having a GetEnumerator method (even if they don't). It will make the F# syntax more expressive and bolster F# competitive strengths in writing clear and concise code.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12564057)**


## Comments ##

