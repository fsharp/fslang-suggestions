# Modify Option.map return None in case of null [8696917] #

**Submitted by Brad Collins on 7/3/2015 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

Java 8's methods on Optional return None in case any operation yields null. Case in point is Optional.map.
Assume that a Session type has a User property that could be null. The following should return None instead of Some(null):
Some(app) |> Option.map (fun a -> a.Session)
The use case is when interoperating with C#, where nulls are more common.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

See above response
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8696917)**


## Comments ##


#### Comment by Mauricio Scheffer on 7/7/2015 3:51:00 PM ####
That would break the functor law "fmap id = id". Java can sort of get away with it (though I haven't seen any formal analysis of this) because you can't construct the equivalent of Some(null), but as we know that's not the case in F#.


#### Comment by Brad Collins on 7/10/2015 2:14:00 PM ####
I see. I didn't think about the algebraic laws. I was coming from Java 8 in which their Optional type does handle null by converting it to a None (or Empty, in Java parlance). F#'s new Option.ofObj() is probably sufficient.
Also, my apologies for my code sample in the original post. I was working with some sample code in which you could walk the property tree this way:
app.Session.User.Name
I accidentally posted the app.Session code snippet instead of the session.User snippet. My apologies for being confusing.


#### Comment by Don Syme on 7/17/2015 6:10:00 AM ####
The current behaviour is appropriate for F# - if the type being returned has null as a true value - or even an abnormal value - then we preserve that.


#### Comment by Mauricio Scheffer on 9/1/2015 7:19:00 AM ####
Here's an article explaining in detail what I briefly mentioned in my previous comment: https://developer.atlassian.com/blog/2015/08/optional-broken/

