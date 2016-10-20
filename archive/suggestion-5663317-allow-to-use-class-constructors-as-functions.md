# Allow to use class constructors as functions [5663317] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**124 votes on UserVoice prior to migration**  

DU case constructors can be used as standalone functions, which means I can use them in partial application:
x |> List.map Some
The same isn't currently allowed on class constructors:
x |> List.map Uri
For this examples is not a problem, but in some real life scenarios is annoying to have to create wrapper functions



## Response ##
** by fslang-admin on 11/12/2014 12:00:00 AM **

This is now completed and available in preview releases of F# 4.0.
For an early Visual Studio preview release see here (cross platform releases will follow) – http://blogs.msdn.com/b/fsharpteam/archive/2014/11/12/announcing-a-preview-of-f-4-0-and-the-visual-f-tools-in-vs-2015.aspx
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663317)**


## Comments ##


#### Comment by Jon Harrop on 3/26/2014 9:42:00 AM ####
Yes, this would be very useful. Strange that you can "|> set" for a set but you have to do "|> fun kvs -> Map kvs" for a Map.


#### Comment by David Grenier on 6/25/2014 8:51:00 AM ####
Curious to know how difficult it would be to extend efforts in this area to allow DUs with "multiple argument" work like Haskell and spare us the need for a tuple? I feel this latter feature is even more useful than the former, esp. with respect to pattern matching.


#### Comment by Richard Minerich on 6/27/2014 1:46:00 PM ####
I think this is a reasonable idea, one thing I've done in the past is to make a factory function with the same name as the class in the same module. This seems to work fairly well (if my memory serves).


#### Comment by Don Syme on 7/10/2014 10:05:00 AM ####
An implementation of this feature has now been submitted here: https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7104


#### Comment by Don Syme on 7/10/2014 10:11:00 AM ####
Note that after this change, the names "Set" and "Map can be used, since they are type names in an auto-opened part of the FSharp.Core library, for example:
let f3() = ["a"] |> Set
let f4() = [("a", 4); ("b", 5) ] |> Map
This is quite regular.
However this does raise the question as to whether the pervasive function "set" (lower case) should be deprecated: it's precisely the same as the above. It is better to have only one way to do things.


#### Comment by Gustavo Guerra on 7/10/2014 10:41:00 AM ####
Will it also work when there's more than one param and/or multiple overloads?
The lower case set (and possible other similar functions) will become redundant, but that shouldn't be a big deal IMHO. There's other things that are way more annoying (like partial application unfriendly param order on Array.get, defaultArg and others because of ocaml compat).
I wouldn't deprecate as it's probably used a lot

