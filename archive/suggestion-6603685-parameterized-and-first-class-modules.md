# Parameterized and First Class Modules [6603685] #

**Submitted by Jared Hester on 10/23/2014 12:00:00 AM**  
**55 votes on UserVoice prior to migration**  

Extend the F# module system to allow paramaterization via functors (that's why the keyword is reserved right?)
First class modules where a module declared with an abbreviation/alias is equal to a module declared with the original module name (unlike OCaml)
It seems like a more robust module system would provide a functional alternative to MEF with a cleaner abstraction model.
Perhaps the `pure` keyword could be used in conjunction with `functor` to enforce a restraint against immutability to ensure the functor is applicative?
See "F-ing modules"
http://www.mpi-sws.org/~rossberg/papers/Rossberg,%20Russo,%20Dreyer%20-%20F-ing%20Modules%20%5BJFP%20Draft%5D.pdf



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declining per my comment below,
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6603685)**


## Comments ##


#### Comment by Ryan Riley on 10/26/2014 6:05:00 PM ####
Is this roughly the same as /archive/suggestion-5664242-simulate-higher-kinded-polymorphism ?


#### Comment by Ryan Riley on 10/26/2014 6:10:00 PM ####
Alternatively, is /archive/suggestion-5665042-allow-extension-interfaces another good possibility that would work with more .NET libraries?


#### Comment by Don Syme on 2/3/2016 2:09:00 PM ####
The decision not to support functors and first class module values in F# is a long standing one.
There are several reasons for this. First, it brings quite a lot of complexity. Second, it can require features like higher kinded type parameters in .NET, or else requires artificial limitations on the functor feature. Third, the feature tends to sit uncomfortably with other features (or potential features) such as object programming, interface types, constraints and type classes.
My inclination is to not revisit this. However keeping this issue open is useful as a way to measure the level of interest in this feature.

