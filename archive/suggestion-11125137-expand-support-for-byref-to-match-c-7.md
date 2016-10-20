# Expand support for byref to match C# 7 [11125137] #

**Submitted by Keith Battocchi on 12/17/2015 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

C# is adding support for byref locals and returns (see https://github.com/dotnet/roslyn/issues/118, slated for milestone 1.3). This will result in many libraries that expose these features (which the CLR already supports), but methods with such return types aren't currently usable from F#. F# already supports byref locals, but doesn't support implementing byref-returning methods nor does it support calling byref-returning methods.
At a minimum, F# should support calling byref-returning-methods (e.g. SomeRefReturningMethod(x,y,z) <- w), since C# users will be creating methods like these and being unable to call them will limit F#'s reach.
It would be nice if on top of that base level of support F# also supported declaring such methods, using the same safety rules that C# is using (e.g. the only refs that are safe to return are those that point to values stored on the heap or existing refs that are passed into the method).



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

Yes, this should be done, thanks
Approved in primciple subject to a detailed design, resolution of any remaining issues, and an implementation, with testing. Also subject to the feature actually appearing in C# 7 :)
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11125137)**


## Comments ##


#### Comment by Keith Battocchi on 12/17/2015 10:40:00 AM ####
Concretely, this code works today:
let array = [| 1 .. 10 |]
let r = &array.[0]
r <- -1
But if you create a method using ildasm that wraps int[]'s Address method (with signature int[] * int -> int&), then this doesn't
let arr = [| 1 .. 10 |]
let r = ArrayHelper.GetAddress(arr, 0) // error FS0412: A type instantiation involves a byref type. This is not permitted by the rules of Common IL.
r <- -1


#### Comment by exercitus vir on 7/2/2016 7:06:00 AM ####
Would it be possible to simply return a `byref` type to implement this feature?

