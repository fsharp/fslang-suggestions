# Modules and Namespaces seem kind of redundant and are confusing at times. Maybe it would be an idea if a module were implicitly a namespace. [8016057] #

**Submitted by Ruffian Eo on 5/18/2015 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

The all different approaches which need to be taken for either targeting an F# only audience or a generic .NET audience cannot be entirely made invisible. Yet, when writing code in F# the question "Namespace or Module or both?" is annoying to bits. Not that anyone really cares or wants to spend time and energy pondering these questions. If a Module were internally implicitly treated as if also being a namespace, some of those quirks might go away and people could write modules by default.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for rationale and discussion see the comments.
Further discussion welcome.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8016057)**


## Comments ##


#### Comment by Christopher Stevenson on 5/31/2015 12:46:00 AM ####
It's worth noting in MSIL, all methods have to be within a class. There are no namespace level functions.


#### Comment by exercitus vir on 6/12/2015 6:37:00 PM ####
Elaborating on Christopher's comment: This is required for other languages to use namespaces or modules written in F#. For example, namespace will still be namespaces in C#, but modules are compiled to a static class. You cannot "import" static classes like you can entire namespaces in C#.


#### Comment by Don Syme on 7/18/2015 5:17:00 AM ####
We considered this at length in the F# 1.x-2.0 design process in 2006-2009. In the end, we decided not to support namespace level values and functions, but instead allowed "module M" declarations at the head of a file. Any compilation mapping for values-and-functions-in-namespaces would cause technical difficulties and the tradeoff came down on the side of the current design.

