# Extend custom numeric types to support floating point literals [8140617] #

**Submitted by Phillip Trelford on 5/27/2015 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

Currently you can define custom numeric types for integer values.
It would be nice to be able to handle floating point values too, e.g.
type complex = Complex of double * double
type imaginery = Imaginery of double
with
static member (+) (lhs:double,Imaginery(rhs)) = Complex(lhs,rhs)
module NumericLiteralI =
let FromZero () = Imaginery 0.0
let FromOne () = Imaginery 1.0
let FromInt32 (x) = Imaginery (double x)
let FromInt64 (x:int64) = Imaginery (double x)
let FromDouble (x:float) = Imaginery x // extension
let polar = 1.5 + 2.5I



## Response ##
** by fslang-admin on 3/4/2016 12:00:00 AM **

Now marking as planned, which means we can move to an RFC https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
The details remain to be worked out however
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8140617)**


## Comments ##


#### Comment by trek42 on 6/6/2015 7:19:00 PM ####
This will be a very desired feature now that Xamarin unified API uses 'System.nfloat' to represent native float type and no longer uses either float or double. Because of this, I have to keep writing "nfloat <float-literal>" (e.g. "nfloat 2.0") for all float literals of nfloat type. It will greatly improve clarity and avoid verbosity if I could just say "2.0nf" where 'nf' denotes native float values.


#### Comment by Don Syme on 7/17/2015 6:45:00 AM ####
This is a nice suggestion - the Xamarin use-case below is of particular interest.
I'm not marking it as "approved" as yet but I'd be interested in seeing a pull request ironing out any lurking design details.


#### Comment by Abel on 2/5/2016 8:26:00 AM ####
@fsharporg-lang: The link to the suggestion "in favour of" is actually *this* suggestion. It seems that you mean to say you are actually going to implement this? Or did you mean to point to another suggestion?

