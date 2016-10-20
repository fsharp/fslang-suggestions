# Extend the set of expressions supported in provided methods [6987639] #

**Submitted by Keith Battocchi on 1/20/2015 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

There are some (undocumented) constraints on what kinds of quotations can be returned by a type provider's GetInvokerExpression method. In some cases (e.g. the lack of support for PropertyGet nodes) these missing expression cases have been papered over in the ProvidedTypes wrapper by translation to supported equivalents (e.g. MethodCall).
However, for some other cases (e.g. FieldGet, FieldSet) there is no reasonable translation to supported equivalents, and for others (e.g. LetRecursive) there's only an awkward translation that is much less efficient than a real implementation would be.
Even in the cases where there is a reasonable translation (like PropertyGet mentioned above), it seems like it would make sense for the compiler to support the expression forms directly - at the moment the set of supported expressions seems ad hoc.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Declined per my comment, thanks for the suggestion
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6987639)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 9:28:00 AM ####
We may move to a model where the low-level ITypeProvider interface doesn't actually use quotations, but rather some representation of code which is independent of System.Type (and actually simpler because of that). That would be a good time to revisit this. Until then I'm going to leave things as they are and close this one as part of bookkeeping, thanks

