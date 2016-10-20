# Allow function names to end with a question mark. [12533019] #

**Submitted by Jeff Heon on 3/1/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I find it really elegant in some language where predicate functions can end with a question mark.
Consider `odd? 5` vs `isOdd 5` or `areRelated a b` vs `related? a b`
There might be some reason why it's a terrible idea grammar-wise or something in F#. I'm still very much a newbie I'm afraid. I apologize if it's featured in a FAQ I missed or even here and I search badly.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12533019)**


## Comments ##


#### Comment by Isaac Abraham on 3/6/2016 11:53:00 AM ####
You can get this to work with backtick declarations which let you put lots of stuff e.g. spaces in the declaration e.g.
let ``odd?`` a = a % 2 <> 0
Intellisense in e.g. Visual Studio doesn't work for them though, unfortunately.


#### Comment by Jeff Heon on 3/6/2016 3:53:00 PM ####
That's great to know Isaac. Thank you very much for taking the time to educate me 8)

