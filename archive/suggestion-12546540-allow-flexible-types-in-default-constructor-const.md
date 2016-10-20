# Allow flexible types in default constructor constraint [12546540] #

**Submitted by George on 3/1/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

This would permit,
let ctor<'a when 'a:(new: unit -> #IWebDriver)> : unit -> IWebDriver = ...
versus
let ctor<'a when 'a:(new: unit- > 'a) and 'a :> IWebDriver> = fun () -> new 'a() :> IWebDriver



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12546540)**


## Comments ##

