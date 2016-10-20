# Support bind (e.g. "await") in the middle of expressions, possibly using !! operator [6752948] #

**Submitted by Arash Sahebolamri on 11/21/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

that does the binding implicitly; so that it wouldn't be necessary to bind every monadic expression to a name. In the case of async workflows, it would behave like the C# await keyword.
With this operator, instead of this:
let task= tasync{
let! response = http.GetAsync(uri)
let! string = response.Content.ReadAsStringAsync()
let! res = processAsync(string)
return res
}
it would be possible to write code like this:
let task= tasync{ return !! processAsync(!!(!!http.GetAsync(uri)).Content.ReadAsStringAsync()) }
Or write this:
let t= opt{ return ((!!x) + !!y) / !!z}
instead of this:
let t= opt{
let! xx = x
let! yy = y
let! zz = z
return (xx + yy) / zz
}



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6752948)**


## Comments ##


#### Comment by Wallace Kelly on 5/28/2015 12:11:00 PM ####
In your examples, you have `tasync`. Is that a typo? Or is `tasync` a real thing?


#### Comment by Don Syme on 2/4/2016 5:54:00 PM ####
Wallace - it's a typo I think.

