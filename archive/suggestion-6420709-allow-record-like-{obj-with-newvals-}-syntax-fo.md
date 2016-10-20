# Allow record-like {obj with newvals...} syntax for arbitrary classes [6420709] #

**Submitted by mikero on 9/10/2014 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

The { oldObj with newval1=x ... } syntax is great syntax - I'd like to see it available for other objects, whether they are defined in F# or not.
I suggest:
- If the object has an IRecordClone (or whatever) implementation (or simply an implementation of a required method), then call it first. This would allow the copying of private data, etc. It returns the new object.
- If there was no pre-copy method to call, or after it runs, perform the standard record-like behavior of copying Public properties over to the new object.



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

This is a duplicate of /archive/suggestion-5663704-copy-and-update-on-class-types


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6420709)**


## Comments ##


#### Comment by mikero on 9/10/2014 4:54:00 PM ####
- *Copying all but the override values*
- and finally setting the new values, obviously


#### Comment by mikero on 9/10/2014 5:07:00 PM ####
The related feature is to allow records to take part in inheritance

