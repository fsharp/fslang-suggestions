# Adopt the (C#/ES6) fat arrow "=>" syntax for lambda functions [6961420] #

**Submitted by Tuomas Hietanen on 1/14/2015 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

"x => x+1" is just faster to write than "fun x -> x+1"



## Response ##
** by fslang-admin on 2/14/2015 12:00:00 AM **

This is a duplicate: please move your votes to /archive/suggestion-5663774-remove-fun-keyword-from-lambda-expressions
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6961420)**


## Comments ##


#### Comment by Tuomas Hietanen on 1/14/2015 1:23:00 AM ####
F# is usually succinct, but the "fun"-keyword breaks the flow.


#### Comment by trek42 on 1/15/2015 3:53:00 PM ####
Only be mildly annoyed by the (slight) verbosity of "fun", I prefer to rather use Haskell's notion (\x -> x + 1), instead of the fat arrow.
Having both "->" and "=>" for the same thing makes the code confusing and inconsistent. Having both (fun x -> x + 1) and (\x -> x + 1) is less harmful.


#### Comment by Alexei Odeychuk on 1/16/2015 7:50:00 AM ####
I think "=>" is not faster to write than "->" using any computer keyboard and it makes code look ugly, heavyweight and confusing (with = and >=).


#### Comment by Phylos on 1/18/2015 12:27:00 AM ####
While it may seem rather superficial, the fact that most languages that are adding lambda functions have a simple syntax is starting to make F#s' syntax look a little bit out-dated. I think replacing the "fun" keyword with Haskells' "\" would be a worthwhile change and make F# code cleaner and modern looking. Completely getting rid of the "fun" keyword may be too difficult to do, hence the suggestion of using "\".
Rather embarrassingly, even Java and JavaScript will soon have lambda function declarations that will be more succinct than F#!!!


#### Comment by Grant Crofton on 1/22/2015 4:44:00 AM ####
I agree with trek42


#### Comment by stm on 2/2/2015 11:34:00 AM ####
That's a duplicate, better vote on this:
/archive/suggestion-5663774-remove-fun-keyword-from-lambda-expressions


#### Comment by mikero on 2/11/2015 5:21:00 PM ####
Given the number of lambdas in F# code - made larger by the fact that F# doesn't support expressions with "holes" (_+_) so we need lambdas to re-arrange arguments (unless you are a combinator person), I think the succinctness of => would be nice. It does seem weird that C# code is more functionally succinct. I'd rather see support for (_ + 1) than (\x -> x+1)

