# Make curly braces in record type definition optional [6153846] #

**Submitted by Chojrak on 7/9/2014 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  

Since we have indentation, the braces are not needed. It's a relict of dark ages. It'd be nice to have:
type Person =
FirstName : string
LastName : string
instead of
type Person = {
FirstName : string
LastName : string }



## Response ##
** by fslang-admin on 10/15/2014 12:00:00 AM **

See comments above
Don Syme, BDFL F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6153846)**


## Comments ##


#### Comment by Chojrak on 7/10/2014 11:20:00 AM ####
I would like to extend this suggestion to also cover computation expressions. They are also indented, so curly braces can be thrown out for good!


#### Comment by Loic Denuziere on 8/17/2014 3:05:00 AM ####
The braces are still needed to construct a record value, and I like the visual similarity between the way a type is declared and the way it is used.
As for computation expressions, a brace-less syntax would be ambiguous. Considering that the word that introduces a CE (such as "async" or "seq") is actually not a keyword but an object, and that we can also define custom operations (such as query's "where", "select" and co), it would be impossible to distinguish between a CE and a function call whose arguments are indented on the next line.


#### Comment by Don Syme on 10/15/2014 7:52:00 AM ####
My assessment is that this creates too much ambiguity between classes and records. Records have sufficeintly different semantics (especially with regard to strucutral equality and comparison) that we don't want to conflate these too much.
Also, for symmetry there would need to be matching removal of the braces in expression and patterns, which is not going to be at all easy.
For these reasons I propose to decline.

