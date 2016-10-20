# Revise the reserved keyword list (e.g. remove "method") [7006663] #

**Submitted by Tomas Petricek on 1/24/2015 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

The keyword "method" is currently reserved for future use.
In many web programming scenarios "method" refers to the HTTP method (GET/POST) and the fact that you currently have to escape the keyword and write ``method`` is annoying. Calling function parameter "meth" instead works (though some people may find this an unfortunate naming ;-)), but it is against F# coding guidelines. And furthermore, this only helps when you're defining the API, but sometimes you need to consume C# API that already has "method" as optional argument.
I think that the F# community is quite happy with using the name "member" for declaring all members (including methods, properties and events) and I don't really think there is a need for keeping "method" reserved.



## Response ##
** by fslang-admin on 6/24/2016 12:00:00 AM **

Agreed the list needs revision. Marking as “approved in principle”.
RFC at https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1016-unreserve-keywords.md


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7006663)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 9:11:00 AM ####
Tomas - could you possibly extend the proposal to assess the entire reserved-keyword list please? If we're going to revise the list, we should do it wholesale.
cheers!
don


#### Comment by Gusty on 9/29/2015 10:09:00 AM ####
I agree, to be fair all reserved keywords should be reviewed. For instance I would be very happy to have keywords available like 'const' which is a very common combinator. If it is not included in the F# core at least give us the option to define it in our libs. Can we also extend the review to operators? Why is $ alone allowed but not composed with other operators?

