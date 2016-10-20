# Allow overloads of custom keywords in computation expressions [12839142] #

**Submitted by Pierre Irrmann on 3/7/2016 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

I've been using custom keywords in computation expressions to write DSLs, and I would have loved to be able to have several signatures for the same custom keyword, in order to make some arguments optional in the expression.
When you try do it today, there is an error message such as "The custom operation 'myOperation' refers to a method which is overloaded. The implementations of custom operations may not be overloaded"
I'm aware this is a not-so-used feature, but I'd like to know how hard you think it could be (I would event be willing to have a look at how to implement it).



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12839142)**


## Comments ##


#### Comment by Jared Hester on 6/28/2016 12:26:00 AM ####
This would be great. If custom operators could take other custom operators as arguments it'd be even better.

