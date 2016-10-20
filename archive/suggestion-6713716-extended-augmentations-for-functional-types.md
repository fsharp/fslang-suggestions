# Extended augmentations for functional types [6713716] #

**Submitted by Greg Chapman on 11/13/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

When working with F#'s "functional" types (e.g., records and unions), I
have often wished that one could organize a module like:
| Functional Type Declarations (without augmentations)
| Functions manipulating the declared types
| Augmentations for the declared types (e.g., with equality and
comparison defined using the functions declared above).
I have particularly wanted this when the types are mutually recursive; I
believe in that case it is much clearer to be able to define the types
alone without mixing in the code from augmentations.



## Response ##
** by fslang-admin on 2/14/2015 12:00:00 AM **

Yes, this can be done today, as per the comment from Marc Sigrist
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6713716)**


## Comments ##


#### Comment by Marc Sigrist on 11/26/2014 5:19:00 AM ####
You can actually do this already now, using intrinsic extensions (see http://msdn.microsoft.com/en-us/library/dd233211.aspx). As long as the extensions are defined in the same file, they are compiled as "real" members of the type.


#### Comment by Greg Chapman on 2/14/2015 1:05:00 PM ####
For completeness, I'll just note that an augmentation (even in the same file) cannot provide an interface implementation (and so cannot provide an IComparable for a [<CustomComparison>] type). Also, providing an Equals override in an augmentation results in a deprecation warning.

