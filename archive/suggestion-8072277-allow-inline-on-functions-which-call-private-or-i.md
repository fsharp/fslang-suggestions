# Allow inline on functions which call private or internal union cases [8072277] #

**Submitted by exercitus vir on 5/21/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

A lot of time you we to ensure a valid construction of union types by making its cases private or internal. E.g.
```F#
type e_mail = private e_mail of string
let inline e_mail_from_string s =
if s |> is_valid //checks e-mail is in valid format
then s |> e_mail |> Some
else None
```
This ensure that values of type e_mail are in a valid format, but this sample does not compile because inline is not allowed on functions which call private or internal functions such as the single case of the e_mail discriminated union.
This restriction should be removed for cases of discriminated unions because a lot of times functions are simply unwrapping the values of single case unions or doing very little work that does not warrant a virtual dispatch.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8072277)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 6:50:00 AM ####
Why not just add a static member to the union type which does the validation?
Also, allowing inlining would break the abstraction boundary defined by private/internal. Using a static member associated with the type -or using "internal" instead of "private" seems adequate.
I will mark this one as declined because allowing inline to break abstraction boundaries would be a significant departure for F# language design.


#### Comment by exercitus vir on 7/17/2015 11:09:00 AM ####
Good point. Thanks for the explanation. I now understand the reason.

