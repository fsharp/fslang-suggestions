# Weight code translation complexity [9161242] #

**Submitted by Marco Falda on 8/4/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Some data types of the F# language are translated in a complex way using classes (e.g.: discriminated unions), while other types could have "hidden" costs, for instance non-structural equality/comparison operators or heap allocated structures. It would be nice to add a sort of profile mode to show how many low level instructions (CIL?), weighted according to their efficiency, are required for translating each F# line, like the "-a" command line option of Cython; look at the bottom of this page: http://docs.cython.org/src/quickstart/cythonize.html.



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

Thanks for the suggestion.
I think the best place to implement such a feature would be in FSharpLint or some other upstack tooling, rather than the language/compiler itself.
Many thanks
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9161242)**


## Comments ##

