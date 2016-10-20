# Lazy properties [7211642] #

**Submitted by Greg Rosenbaum on 3/14/2015 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

A big problem of records and discriminated unions is that they cannot store computed ("memoized") data. For example, you cannot have a linked list store its own length without having it as a constructor parameter (which has obvious problems). The ability to cache computed data is a big advantage of immutable objects, because the data will never change and thus never needs to be recalculated.
A very simple and elegant solution to this problem is having lazy properties. A lazy property is backed by lazy<'a> field behind the scenes. Here is an example of syntax: https://gist.github.com/Springwight/ae423184487a1d6fc831



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7211642)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 7:35:00 AM ####
While I appreciate the effort to make common tasks simple, as it stands I don't think this suggestion fits well with the F# language design.
- Adding "lazy" to a member would bee odd, since members are already computed on-demand.
- It is fairly easy to amortize a member in a class by adding an explicit "let x = lazy ..." binding. In a record, an auxiliary class containing static data can be used.
- There are several ways to implement laziness (e.g. is a lock taken during execution, is a "null" used to indicate a not-yet-computed value etc.) and it is in general better to make this explicit - apart from the built-in "lazy" for expression level constructs.
Lastly, I guess it goes without saying that there is a very high bar for new declaration constructs since effectively all F# programmers will need to understand them.

