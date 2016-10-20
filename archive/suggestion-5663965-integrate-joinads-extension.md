# Integrate joinads extension [5663965] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**121 votes on UserVoice prior to migration**  





## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

I’ve discussed this with Tomas today and he agreed it’s best to mark this as “declined” for now.
It wasn’t too political! Honest!!!! :)
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663965)**


## Comments ##


#### Comment by Richard Minerich on 3/21/2014 4:41:00 PM ####
You can try joinads here: http://tryjoinads.org/
It's already done, and from what I can tell seems to work great! What's holding this one back?


#### Comment by thinkb4coding on 4/4/2014 6:56:00 AM ####
Joinads extend the computation expressions with the match! keyword to give control over the pattern matching to the underlying builder.
let putString = Channel<string>()
let putInt = Channel<int>()
let getString = ReplyChannel<string>()
join {
match! getString, putString, putInt with
| repl, v, ? -> repl.Reply("Echo " + v)
| repl, ?, v -> repl.Reply("Echo " + (string v)) }
It becomes more and more useful for reactive applications and frameworks like Orleans, Akka.net and Rx extensions, to implement flexible pattern matching on messages.
Applicative functors add 'let! x = xs and y =ys' and 'for x in xs and y in ys do ...' and enable to build zip semantic over computation expressions that can also prove useful in reactive applications, computations on time series, and much more:
let totalPrice =
timeseries {
for p in unitPrice
and q in quantity
yield p * q
Both have been implemented for F# 3.0 open source on Tomas Petricek and my research branch:
https://github.com/tpetricek/fsharp/commits/research
https://github.com/thinkbeforecoding/fsharp/commits/research
a first implementation based on F# 2.0 can be tested at http://tryjoinads.org/


#### Comment by Bryan Edds on 4/8/2014 9:01:00 AM ####
I'm with Richard here - I too wonder what's holding this one back?


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/6/2014 8:47:00 AM ####
I don't know why this has not been incorporated.


#### Comment by Nicolas R on 6/13/2014 8:22:00 AM ####
I think it is tricky to prove it correct and this is not a small change. although I am not quite informed. concurrent programming is really valuable though.


#### Comment by Lev Gorodinski on 4/21/2015 4:14:00 PM ####
Would it be simpler to only support active patterns than can return `Choice` but wrapped in a type? For example:
let (|Left|Right|) (a:Async<'a>, b:Async<'b>) = async {
let! first,second = Async.choose (Choice1Of2 a) (Choice2Of2 b)
match first with
| Choice1Of2 a -> return Left a
| Choice2Of2 b -> return Right b
}
and use like:
match! a,b with
| Left a ->
| Right b ->


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 8/15/2015 12:12:00 AM ####
I would guess that it might be internal politics within the F# team which might be holding this back. I do not know for sure though.


#### Comment by Don Syme on 2/3/2016 12:53:00 PM ####
I think my position on joinads is fairly well known. The proposal is most definitely interesting from a research language design perspective.
However the typical "bang for buck" tradeoff analysis just doesn't convince me that this should be in F# itself.


#### Comment by Dax Fohl on 6/18/2016 10:20:00 PM ####
@DonSyme Your position is not well-known in the larger F# world, which is actually quite large now. Can you comment more about where you see the "bang" and the "buck"? I see some potentially useful ideas from tomasp's blogs, but not sure where the buck lands. Does it kill compiler time, or...?

