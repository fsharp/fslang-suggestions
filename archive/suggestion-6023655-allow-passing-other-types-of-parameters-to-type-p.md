# Allow passing other types of parameters to type providers [6023655] #

**Submitted by Loic Denuziere on 6/8/2014 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

It would be very useful to be able to pass lists, arrays, options, tuples as static parameters to type providers. Something like this:
type Foo = FooProvider<files = ["file1.txt"; "file2.txt"]>
Note that this is different from /archive/suggestion-5675977-allow-type-providers-to-generate-types-from-other which is about taking *types* as parameter; this is about taking *values* of a few specific predefined types, which should be much simpler as it doesn't need staged compilation.



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Declined per my comment below, in favour of two other suggestions
Thanks
Don


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6023655)**


## Comments ##


#### Comment by Don Syme on 2/10/2016 11:25:00 AM ####
I am going to decline this. If we did something more in this area it would be to allow System.Type and arbitrary quotation expressions to be passed as arguments. These are covered by /archive/suggestion-8306538-allow-quotations-of-expressions-used-as-type-provi and /archive/suggestion-5675977-allow-type-providers-to-generate-types-from-other

