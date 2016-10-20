# Support mixed F# and C# projects in order to extend F# usage [14795655] #

**Submitted by zjv on 6/13/2016 12:00:00 AM**  
**121 votes on UserVoice prior to migration**  

Support mixing F# and C# source files in the same project in order to support a gradual move to F# for new users/organisations and to support cases where tooling is oriented at C# (F# not supported)
For instance I could use this feature to slowly move a C# project to F# one class at the time. Another example would be to use C# tooling to generate web infrastructure like ASP.NET 5 controllers (because F# does not currently have templates for this) and then call directly into F# from those.
P.S. Other languages that F# compares to like Scala already supported mixed projects



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14795655)**


## Comments ##


#### Comment by Anonymous on 7/5/2016 8:33:00 PM ####
Nemerle's support for mixed C# and Nemerle source files was a very appealing feature when I first found it. Although the Nemerle compiler was built as something like a fork of the C# compiler. I would be much more inclined to use F# if I didn't have to 100% commit to it. As functional as C# is getting, it would be nice at times to leave the C behind.


#### Comment by Gauthier Segay on 7/5/2016 9:31:00 PM ####
I think kotlin has such support with java too.
I'd see this idea coming to fruition first in scripting:
#load @"path/to/file.csx"
where it is easy to figure out the topoligical graph of script files to include, compile in separate assemblies and link.
If this is made, then work on same feature in project system would be great.
I think that would also give few kicks to Jetbrains to finally start implementing F# support and more importantly, this would restore some trust in having the whole of MS people working on .NET focused on making best platform with highest level of interop among all the languages, having them invest major engineering efforts which benefits all the languages (current and future) to have easy embedding of all IL compilers in a meta compiler.
F# file ordering is also a major aspect making this seem viable.


#### Comment by mmc on 7/16/2016 11:29:00 AM ####
Another valuable usecase for this would be to F# projects that needs to be consumed from other .NET languages like C#. A mixed F# project could have all the private logic as F# files but the main exposed interfaces as C#.


#### Comment by Charles Roddie on 9/21/2016 8:39:00 AM ####
How is this compatible with file order requirements?
1.cs, 2.fs, 3.fs, 4.cs
Presumably the fs files can refer to previous cs files, and the cs files can refer to each other. Then 2.fs can refer to 1.cs which can refer to 4.cs which can refer to 3.fs. So 2.fs can effectively refer to 3.fs and the whole linear order of F# is broken, isn't it?


#### Comment by Gauthier Segay on 9/21/2016 2:41:00 PM ####
Charles Roddie, this would work with "islands" of C# files compiled together and knowing about previous compiled islands, 1.cs can't know about 4.cs in your case.

