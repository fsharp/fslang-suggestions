# Allow type annotations at the top level in fsi [16126906] #

**Submitted by Loic Denuziere on 9/16/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Currently, using a type annotation at the top level in fsi results in a syntax error:
> 1 : int;;
1 : int;;
--^
stdin(1,3): error FS0010: Unexpected symbol ':' in interaction. Expected incomplete structured construct at or before this point, ';', ';;' or other token.
The workaround is to wrap the whole expression in parentheses, but I don't believe there's any reason for it to be necessary. It has misled some people into thinking they need to use another syntax instead (I've seen people try to use :?> for example).



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/16126906)**


## Comments ##

