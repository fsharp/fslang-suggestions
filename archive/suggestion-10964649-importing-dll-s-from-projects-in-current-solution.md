# Importing DLL's from projects in current solution into F# interactive [10964649] #

**Submitted by zjv on 12/4/2015 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

It is currently a hassle to import references to DLL's from projects in the current solution because full paths has to be given and recursive dependencies have to be handled manually. Why not make it possible to import a "project" by name along with all dependencies into F# interactive.



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

See comment above


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10964649)**


## Comments ##


#### Comment by Eric Stokes on 12/31/2015 11:13:00 PM ####
Or at least remove the requirement that references be entered in dependency order to fsi. Error FS0074 is a big pain point for me in fsi, and there are numerous confused discussions about it on stackoverflow and github. I realize this may not be that easy, but it would be worth the effort!


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 1/23/2016 11:43:00 AM ####
This is implemented as "Send project references to F# Interactive" in Visual Studio, and I think may be available similarly in other F# tooling. So I will mark it as completed
In any case it is more on the tooling side than the language side.

