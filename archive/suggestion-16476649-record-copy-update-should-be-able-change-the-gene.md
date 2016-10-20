# Record copy update should be able change the generic type [16476649] #

**Submitted by Marko Grdinic on 10/3/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

type A<'a> =
{
mutable x: 'a
}
let a = {x = 1}
{a with x="Hello"} // Type error
Since the x field is generic and F# is type safe, it would not be bad if the above was valid.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/16476649)**


## Comments ##

