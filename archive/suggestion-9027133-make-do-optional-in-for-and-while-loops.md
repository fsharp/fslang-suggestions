# Make "do" optional in for and while loops [9027133] #

**Submitted by Phillip Trelford on 7/26/2015 12:00:00 AM**  
**43 votes on UserVoice prior to migration**  

Currently all for and while loops must specify "do" before the statements:
for i = 1 to 10 do
printfn "Hello World"
This does not feel intuitive for developers coming from Python or BASIC. The "do" should not be required by the parser as for example "in" is no longer required in the default light syntax mode.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

See my comment below
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9027133)**


## Comments ##


#### Comment by luketopia on 8/17/2015 6:53:00 PM ####
I sometimes forget the "then" on an if/else/elif and wonder if it could be made optional along the same lines. Only other thing I can think of that is like this is the "with" in a match expression, though I kind of like one that for some reason.


#### Comment by Bryan Edds on 8/23/2015 8:30:00 AM ####
Oppose. This is of little utility, and does not jibe with the way ML parsing is intended to work. Same opposition applies to optional 'then'.


#### Comment by Bryan Edds on 8/23/2015 8:31:00 AM ####
Also oppose due to the inconsistency this will create among code bases and styles so late in the game. It just isn't buying us much.


#### Comment by Richard Gibson on 8/27/2015 9:19:00 AM ####
I don't think this is even possible. You need the `do` keyword to separate the `for` expressions from the code that is being executed in the loop.
Using your example, you would like to write:
for i = 1 to count printfn "Hello world"
Did you mean:
for i = 1 to count do printfn "Hello world"
or:
for i = 1 to (count printfn "hello world") do ...


#### Comment by Phillip Trelford on 11/11/2015 3:59:00 AM ####
Richard, I'd expect the `do` keyword may still be used when writing multiple statements on a single line, just as the `in` keyword is still required in F# in this scenario. This is how Ruby approaches while & for loops, see http://www.tutorialspoint.com/ruby/ruby_loops.htm


#### Comment by Don Syme on 2/3/2016 12:13:00 PM ####
I do understand that Python and BASIC users may find the extra "do" and "then" keywords non-intuitive. In a different world, we may have opted to use ":" or some other line-terminator.
However, I think this decision is now fixed in stone for F#, I don't see us making this specific change in anything but a wholesale revision of the language syntax, which is not on the agenda any time soon.
So I'm marking this as declined.

