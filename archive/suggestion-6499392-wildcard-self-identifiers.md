# Wildcard self identifiers [6499392] #

**Submitted by Daniel Robinson on 9/29/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

Two underscores are frequently used in member definitions to denote an ignored "self" identifier. This seems like a hack given that the language already provides a wildcard pattern that represents an unused value.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

I’m marking this as approved in principle for F# 4.×. you are invited to submit a quality and tested implementation would be needed, to be submitted to http://github.com/Microsoft/visualfsharp.
See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for details about contributing to the F# language and core library
FWIW I’ve actually taken a look at this once or twice and it was surprisingly invasive to implement. But by all means give it a go and ask if you need help.
Don Syme
BDFL F# Language/Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6499392)**


## Comments ##


#### Comment by Daniel Robinson on 9/29/2014 11:16:00 AM ####
Forgot the link to the old VS UserVoice item: https://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/3745318-allow-wildcard-self-identifiers


#### Comment by Alexei Odeychuk on 10/10/2014 1:48:00 AM ####
I think one underscore is enough to denote an unused "self" identifier. The language has to be consistent. One underscore has already been in use to denote an unused value in the match expression.


#### Comment by Daniel Robinson on 10/15/2014 4:59:00 PM ####
Thanks for the invitation. I hope to be able to contribute to the F# tools eventually, but my schedule won't allow it at present. Hopefully someone else will be willing to take this on.


#### Comment by Richard Gibson on 11/26/2014 6:50:00 AM ####
Are self-identifiers actually needed at all? I know they're in there for historical reasons, but I don't see any actual use for them.
Considering F# still has the "base" keyword, I see no reason we can't use the normal "this" as well.


#### Comment by Daniel Robinson on 12/8/2014 10:43:00 AM ####
Richard, here's one use: http://stackoverflow.com/a/5356224/162396


#### Comment by exercitus vir on 7/20/2015 10:34:00 PM ####
Isn't a single underscore just a convention? You can use any other lower-case letter or non-letter-character as a last match to match anything. It seems that the underscore itself has no special meaning in F# other than being allowed as type parameters without leading '.

