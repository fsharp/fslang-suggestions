# Support Multiple Properties in StructuredFormatDisplayAttribute [7099985] #

**Submitted by Sven Grosen on 2/15/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

There's currently a limitation in StructuredFormatDisplayAttribute whereby you can only provide a single property in the Value.
So for a type like this: type Person = {First: string; Last: string} I have to create another property like FullName to use in StructuredFormatDisplayAttribute. The fix/enhancement should be easy to do, and something I could probably just do myself.
I first broached this subject on StackOverflow and Tomas Petricek suggested I create an issue for this. Here's the link to the SO question: http://stackoverflow.com/questions/28505368/can-i-use-multiple-properties-in-a-structuredformatdisplayattribute



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

See comments – in F# 4.0


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7099985)**


## Comments ##


#### Comment by exercitus vir on 5/21/2015 6:09:00 PM ####
This is planned for F# 4.0: http://blogs.msdn.com/b/dotnet/archive/2015/04/29/rounding-out-visual-f-4-0-in-vs-2015-rc.aspx
See section "Multiple properties in [<StructuredFormatDisplay>]"

