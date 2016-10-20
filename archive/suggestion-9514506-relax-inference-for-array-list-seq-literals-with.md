# Relax inference for array/list/seq literals with #subtypes [9514506] #

**Submitted by Loic Denuziere on 8/27/2015 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

See here for some context: http://websharper.com/question/80117/allow-doc-element-to-take-seq-doc-children
Currently, if the context decides that a given array/list/seq literal has type seq<#T> (for example if it is passed to a function that expects that), then the exact subtype of T is decided by the first element of the sequence, and if any subsequent element is more general then it is a type error. It would be nice if the type could be generalized instead.
Example:
type Animal() = class end
type Dog() = inherit Animal()
let feed (animals: seq<#Animal>) = ()
// Type error on `Animal()`: expected Dog, got Animal
feed [ Dog(); Animal() ]



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Per my comment, the example works if you drop the use of # flexibility in this case
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9514506)**


## Comments ##


#### Comment by Robert Kuzelj on 11/1/2015 12:21:00 PM ####
This is my biggest pain when interfacing with other (class based) libraries in F#.
It makes almost impossible to write even the lightest functional wrapper around such libraries. except one start to wrap all child classes into distinct union value constructors.


#### Comment by Don Syme on 2/5/2016 6:10:00 AM ####
The example works if you just drop the # flexibility: https://gist.github.com/dsyme/a02b19b9e55ab392a06d


#### Comment by Don Syme on 2/5/2016 6:12:00 AM ####
I will mark this particular request as declined because it's not entirely clear what is being proposed here. Please reopen with a more concrete suggestion and lots of examples? I understand there is pain in this area but we need further motivating examples.
Thanks!

