# #r URLs [5665226] #

**Submitted by Jon Harrop on 3/21/2014 12:00:00 AM**  
**18 votes on UserVoice prior to migration**  

Allow #r in scripts to reference on-line scripts via URLs.



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Unfortunately as much as I like this I have to mark it declined for the reason mentioned below
Don Syme,
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5665226)**


## Comments ##


#### Comment by Richard Minerich on 3/21/2014 4:34:00 PM ####
We do something like that with a project at Bayard Rock, except we use #N for nuget and it automatically goes and gets it, and pulls in the correct references for the specific version of the runtime.
We'll be adding it to the ipython F# profile soon.


#### Comment by Gustavo Guerra on 3/21/2014 5:05:00 PM ####
Would be great to have this for NuGet


#### Comment by Jon Harrop on 3/21/2014 5:27:00 PM ####
Ok. I think this is *much* simpler than referencing a Nuget package.


#### Comment by Robert Jeppesen on 3/21/2014 8:13:00 PM ####
+3 Simple, beautiful.


#### Comment by Don Syme on 2/10/2016 11:08:00 AM ####
I think this is not allowed in a Microsoft programming model for security reasons (a scripting referencing a malicious DLL can be sent around, and even the act of opening the script might compromise things if the referenced DLL contains a type provider).

