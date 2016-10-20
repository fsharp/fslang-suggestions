# Extend named DUs syntax to allow to use multiple names in a name match [5663194] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Currently when I have a DU like this:
type DU =
| Case1 of prop1:string * prop2:ing * prop3:bool
...
I can pattern match like this:
| Case1(prop1 = "foo")
but I can't like this:
| Case1(prop1 = "foo", prop3 = false)



## Response ##
** by fslang-admin on 3/21/2014 12:00:00 AM **

This is already in F# 3.1, as noted, closing to recycle votes


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663194)**


## Comments ##


#### Comment by Don Syme on 3/21/2014 9:54:00 AM ####
Note you can do this via a semi-colon
| Case1(prop1 = "foo"; prop3 = false)
But I agree, this would be better allowed using a comma. The use of semicolon was a design oversight during the implementation of F# 3.1


#### Comment by Gustavo Guerra on 3/21/2014 10:10:00 AM ####
Ah, didn't know about that, both the F# 3.1 announcement post (http://blogs.msdn.com/b/fsharpteam/archive/2013/06/27/announcing-a-pre-release-of-f-3-1-and-the-visual-f-tools-in-visual-studio-2013.aspx) and the msdn docs (http://msdn.microsoft.com/en-us/library/dd233226.aspx) don't mention that
I'm happy with the semicolon, it just needs to be better documented as I doubt many people know about it


#### Comment by Don Syme on 3/21/2014 11:41:00 AM ####
I've updated the blog post with a note about this. Please add feedback to the MSDN docs.

