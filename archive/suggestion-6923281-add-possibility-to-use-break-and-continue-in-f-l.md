# Add possibility to use break and continue in f# loops. And do while loop [6923281] #

**Submitted by Vladimir on 1/5/2015 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

It very often looks better than recursion, and it would be wonderful to have this possibility



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6923281)**


## Comments ##


#### Comment by Vladimir on 1/5/2015 5:50:00 AM ####
And it would be wonderful to add the same things to sequences


#### Comment by Richard Minerich on 1/12/2015 12:05:00 PM ####
I have mixed feelings about this. On one hand there have been cases where having this would be useful for porting code from other languages, on the other I'd be worried that many would start to use these in cases that are more clearly expressed as recursion and in so doing make the code much more difficult to understand and maintain.


#### Comment by Phylos on 1/18/2015 12:32:00 AM ####
I don't think this is a good idea, as it would encourage perpetuating imperative programming approaches to those new to F#.


#### Comment by Vladimir on 2/9/2015 4:08:00 AM ####
but when we working with arrays, it's not so clear to use recursion. Especially, when we must modify the array. In this case recursion looks very ugly, especially, we must send a lot of arguments there.
P.S. I also like functional style, but in some cases imperative style is much better. And it's very sad when I cant use the best way to resolve some problem in my favorite language, and should use for that, for example, c#


#### Comment by Richard Gibson on 2/17/2015 8:39:00 AM ####
I'm also not convinced this is a good idea - most of the time when I was learning F# and I wished for break or continue it was because I didn't know how to use the appropriate F# sequence function yet. `Pick` and `find` are two functions that come to mind in helping get out of the imperative way of thinking.
If you have any examples on where it's truly necessary or preferable to use break / continue I'd love to see them, only because I can't think of any myself.


#### Comment by Vladimir on 3/6/2015 7:04:00 AM ####
Sequences is very slow and there are some situation when performance is required. For example when you work with matrices. Also you can't always use Array module, because its functions always copy array, that is not very well in most cases. So if you can said, how to work with it without recursion, I will be very glad.
I see very often, when some one use "rec loop" for making loops functionality. I think it's awful.
I think if you don't need loops (with break and continue) you can don't to use it. I think it's not a big problem to implement this feature and you can decide for yourself, should you use it or not.

