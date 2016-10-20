# Allow static optimization conditionals [16402732] #

**Submitted by lee on 9/28/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

If we write the code as below, we will get a compile error: Static optimization conditionals are only for use within the F# library
let inline toBytes (x : ^a) : byte[] =
(^a : (static member ToBytes : ^a -> byte[])(x))
when ^a : byte = [|retype x : byte|]
when ^a : string = System.Text.Encoding.UTF8.GetBytes(retype x : string)

But allow "static optimization conditionals" is very useful, which allow us avoid to use those tricks like "Simple typeclass implementation". http://www.fssnip.net/9B



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/16402732)**


## Comments ##


#### Comment by Gusty on 10/1/2016 4:33:00 PM ####
I'm not sure type inference will work well by only allowing static optimizations outside the F# library.
If you look at the source code of the F# compiler there are many particular cases introduced in order to get simulated members working and inferred.
In your example calling toBytes with byte will not type check because byte doesn't have a ToBytes static member.
Anyway there seems to be a better way to implement type classes in .NET http://www.mlworkshop.org/2016-7.pdf?attredirects=0

