# Allow printfn to support repeated arguments [13393365] #

**Submitted by Dave Thomas on 4/12/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Rather than:
printfn "%i %x %A" mySecretNumber mySecretNumber mySecretNumber
Perhaps an index argument could be added
printfn "%[1]i %[1]x %[1]A" mySecretNumber



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13393365)**


## Comments ##


#### Comment by Gauthier Segay on 4/17/2016 8:08:00 PM ####
Dave, do you think that would still be useful with making your variable name short in the scope where you want to print it:
do
(**)let n = mySecretNumber
(**)printfn "%i %x %A" n n n
I think it is interesting idea (but with a 0 based index and robust compiler checks) but maybe not as useful as string interpolation?


#### Comment by Dave Thomas on 4/19/2016 2:34:00 AM ####
I currently use a short variable if I can to reduce the annoyance, but forcing myself to use bad variable names is not good practice either. It seems there should be a way to reuse a binding rather than repeating yourself.


#### Comment by Gauthier Segay on 4/19/2016 6:43:00 AM ####
Dave, can you show how mixed of positional and indexed arguments would play together?
Should we reuse string.format notation with braces?


#### Comment by Yemi Bedu on 5/27/2016 11:24:00 AM ####
Hello,
So if you have the following (0 indexed):
printfn "%A %A[0] %A" a b c
printfn "%A %A[1] %A" a b c
printfn "%A %A %A" a b c
printfn "%A %A %A[1]" a b c
The first and fourth would seem to be a compiler error and the second and third should be okay. It seems like subtle errors can easily creep in that may not be obvious with a quick eye scan. How can this be made more clear or is it better to cancel this in favor the following:
/archive/suggestion-6002107-add-string-interpolation-to-println-syntax-from-s

