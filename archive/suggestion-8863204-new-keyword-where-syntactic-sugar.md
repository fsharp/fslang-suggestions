# New keyword "where" (syntactic sugar) [8863204] #

**Submitted by Dmítrij Jevgénijevič Ačkásov on 7/14/2015 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

Current F# code is very head heavy. Most functions have implementation at the end and predeclarations at the top. The Haskell keyword "where" would help to reverse this relation.
ex:
let ffffffff a b c = let i=5 in (a+b+c)*i
is identical to
ex:
let ffffffff a b c = (a+b+c)*i where let i=5



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Closing issue with zero votes


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8863204)**


## Comments ##

