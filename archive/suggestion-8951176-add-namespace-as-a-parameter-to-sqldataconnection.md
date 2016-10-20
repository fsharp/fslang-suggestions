# Add namespace as a parameter to SqlDataConnection [8951176] #

**Submitted by Anonymous on 7/20/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Right now there doesn't appear to be any way to define a namespace to be passed to SqlMetal. This is problematic when you have a database object named System as it conflicts with System imports/usings.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Moved see below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8951176)**


## Comments ##


#### Comment by luketopia on 7/30/2015 6:56:00 PM ####
I have run into this problem as well. I'm not sure being able to control the namespace provides any benefit since the namespace is only used in the code generation process and the generated types are ultimately relocated / nested under the root provided type. I think that the type provider just needs to pass some dummy namespace when calling SqlMetal rather than nothing as it does now.


#### Comment by Don Syme on 2/3/2016 12:17:00 PM ####
Moved to https://github.com/fsprojects/FSharp.Data.TypeProviders/issues/8

