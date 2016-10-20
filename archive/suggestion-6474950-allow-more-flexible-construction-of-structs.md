# allow more flexible construction of structs [6474950] #

**Submitted by citykid on 9/23/2014 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

in F# it is not possible to have a constructor for a struct that sets only some fields. For structs that have an expicit field layout (low level discriminating unions so to say) this is very prohibiting.
c#
struct Point
{
private readonly int _x;
private readonly int _y;
public Point(int x) : this() // Will set _y = 0, make this possible in fä
{
_x = x;
}
}
f#
type Point =
struct
val X: float
val Y: float
new(x: float, y: float) = { X = x; Y = y }
new(x: float) = ? // how to call this() or new() here? <<<<<<<<======
end



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion! I’ve added links to how you can do this. Declining per my comments
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6474950)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 5:58:00 AM ####
You do this: https://gist.github.com/dsyme/4dc266348f47303f6b99
Our use DefaultValue: https://gist.github.com/dsyme/2fceed8074e56f17a761


#### Comment by Don Syme on 2/5/2016 5:58:00 AM ####
Will close this since you can use the techniques below

