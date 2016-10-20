# Allow extension members in namespaces, without requiring an enclosing module [10921911] #

**Submitted by Alexei Odeychuk on 12/1/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Now it's impossible to declare extension members directly in namespaces, except in the same file and namespace where the type is defined. Please consider eliminating that limitation of the language on the expression of developer's ideas. That limitation does not serve any reasonable purpose, I think. Nobody needs to create a module with [<AutoOpenAttribute>] to hold declarations of extension members only in order to circumvent that limitation of the language. I believe that if a developer needs to create an extension method for a type, he/she should be able to do it directly in any namespace of the application he/she is developing.



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Thanks for the suggestion. I’ve marked it declined, as per the comment below
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10921911)**


## Comments ##


#### Comment by Alexei Odeychuk on 12/1/2015 3:47:00 AM ####
If such a wrapper module is needed for compilation reasons, let the compiler create such a module with [<AutoOpenAttribute>] automatically.


#### Comment by Don Syme on 2/10/2016 11:03:00 AM ####
Because of a considerable amount of technical detail, and because of how extension members are compiled, this is actually quite difficult. As a result I don't think we are going to make this change.

