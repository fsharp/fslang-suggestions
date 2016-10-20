# Allow tuples for overloaded method and constructor arguments [5668239] #

**Submitted by Mark Seemann on 3/22/2014 12:00:00 AM**  
**28 votes on UserVoice prior to migration**  

When a constructor or method isn't overloaded, you can use a tuple as arguments:
open System
let u = Uri("http://blog.ploeh.dk/tags.html#F#-ref")
let pqd = u.GetComponents (UriComponents.PathAndQuery, UriFormat.SafeUnescaped)
let pqargs = (UriComponents.PathAndQuery, UriFormat.SafeUnescaped) // UriComponents * UriFormat
let pqa = u.GetComponents pqargs
let osd = OperatingSystem (PlatformID.Win32NT, Version(1, 2, 3, 4))
let osargs = (PlatformID.Win32NT, Version(1, 2, 3, 4)) // PlatformID * Version
let osa = OperatingSystem osargs
However, when a constructor or method has overloads, it doesn't work:
let vd = Version (1, 2, 3, 4)
let vargs = (1, 2, 3, 4) // int * int * int * int
//let va = Version vargs
//The above line can't compile, but gives this error:
//error FS0001: This expression was expected to have type
// string
//but here has type
// int * int * int * int
let s = "Some piece of text"
let sd = s.StartsWith ("Some", StringComparison.CurrentCulture)
let swargs = ("Some", StringComparison.CurrentCulture) // string * StringComparison
//let sa = s.StartsWith swargs
//The above line can't compile, but gives this error:
//error FS0001: This expression was expected to have type
// string
//but here has type
// string * StringComparison
It would be nice if it also works for overloaded methods, since the tuples seem unambiguous to me.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per my comments below.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5668239)**


## Comments ##


#### Comment by Liviu on 3/23/2014 1:17:00 PM ####
I checked, and Nemerle language supports this feature since ages.


#### Comment by Gustavo Guerra on 6/20/2014 5:08:00 PM ####
Don't have more votes, but +1


#### Comment by Don Syme on 2/3/2016 1:28:00 PM ####
My inclination is not to change the F# behaviour here in the presence of method overloading.
The present design was chosen deliberately to have the programmer remove some of the ambiguity when method overloading, tuples and type inference collide. In overloaded cases we ask the programmer to split into individual arguments.
Also it actually seems relatively rare that it is useful to pass first-class tuples to overloaded methods. The Version example is one case where it happens.

