# Move user settings out of .fsproj file [6564576] #

**Submitted by Robert Jeppesen on 10/15/2014 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

Command line parameters for debugging are stored in the F# project file. This makes it hard to keep your commits clean.
My suggestion is to do the same as C#, where this information is stored in .csproj.user, which is not put in version control.
This doesn't really have anything to do with the language itself, but it *is* part of the package.



## Response ##
** by fslang-admin on 10/20/2014 12:00:00 AM **

Moved as discussed in the notes


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6564576)**


## Comments ##


#### Comment by Steffen Forkmann on 10/15/2014 8:14:00 AM ####
YES! Please do this.


#### Comment by Don Syme on 10/15/2014 12:07:00 PM ####
This is really the Visual F# Tools, and not the F# language or core library.
Please move this to https://visualstudio.uservoice.com/forums/121579-visual-studio/category/30935-languages-f-tools. I think there is already a tracking item there.
Thanks!
Don


#### Comment by Don Syme on 10/15/2014 12:08:00 PM ####
And ideally just make the submit fixes and tests to the Visual F# Tools code, what you request is entirely reasonable :)


#### Comment by Robert Jeppesen on 10/16/2014 3:36:00 AM ####
Moved to https://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/6568436-move-user-settings-out-of-fsproj-file

