# Indentation of new lines should be dependent on the *start* of the previous line, not the end of it [7813977] #

**Submitted by George on 5/4/2015 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

The following layout requires that content after the 'View<' be indented beyond the endding '<' on the following lines which makes the level of indentation dependent on the type name. Which is silly.
[<AbstractClass>]
type View<
'Events,
'Window when
'Window :> Window and
'Window : (new : unit -> 'Window)
>(?window) =
let window = defaultArg window (new 'Window())
member this.Window = window



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Closing in favour of /archive/suggestion-9156844-relax-some-of-the-indentation-rules and linking back here


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7813977)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 1:42:00 PM ####
Could you please post a gist for this that preserves layout?


#### Comment by George on 6/10/2015 11:59:00 AM ####
Here is the gist:
https://gist.github.com/anonymous/18108a3fbaa79433ce65.js


#### Comment by George on 6/10/2015 12:07:00 PM ####
Here is the gist:
https://gist.github.com/anonymous/18108a3fbaa79433ce65
To clarify, FSharp currently imposes indentation constraints based on the occurrence of special delimiting characters in preceding lines. The result is indentation becomes dependent on the selection of identifier names. This constraint also waste space and undermines the ability to structure the source code semantically.


#### Comment by Don Syme on 7/17/2015 7:05:00 AM ####
Hi George,
We could consider "<" as opening a new indentation context. However I think in practice it's unlikely that we would modify the design and implementation of the indentation aware syntax in order to support this.
This is partly because the processing of "<" is already quite complicated because of the disambiguation of " a<b" and "a<b>", and partly because of the stability requirements in the syntax processing.
A pull request to allow this might explore the design space and build confidence and I'd be interested to see one.


#### Comment by Don Syme on 2/3/2016 1:08:00 PM ####
Closing in favour of /archive/suggestion-9156844-relax-some-of-the-indentation-rules

