# #package directive to import NuGet packages in F# interactive [5670137] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**248 votes on UserVoice prior to migration**  

It would be quite useful for F# interactive to support a #package directive to allow NuGet packages to be downloaded from within the REPL. I think it would be best if this directive simply downloaded the package, unpacked it, and automatically included (#I) the correct folder based on the framework version F# interactive is running under (e.g., net45). If a package doesn't include assemblies for the specific framework version F# interactive is using, we'd automatically include the folder for the latest framework version which is compatible; e.g., if running on .NET 4.5 and a package only includes a 'net40' folder, we'd include (#I) that folder. I believe this behavior is consistent with how NuGet currently works when referencing packages from a project, e.g., in Visual Studio.
#package should not, however, automatically reference (#r) the assemblies included in the package, in case you only want to reference some of them.
Here's a usage example:
#package "ExtCore.0.8.41"
#r "ExtCore.dll";;
let substr = substring "Hello World!"
printfn "Value: %O" substr;;



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670137)**


## Comments ##


#### Comment by Jon Harrop on 3/26/2014 8:46:00 AM ####
Yes!


#### Comment by Christoph Rüegg on 4/23/2014 12:50:00 PM ####
See also: https://visualfsharp.codeplex.com/workitem/42


#### Comment by Greg Chernis on 9/15/2014 8:03:00 PM ####
Here's a workaround: http://tobivnext.wordpress.com/2014/03/26/import-nuget-packages-to-fs-interactive/


#### Comment by Don Syme on 2/14/2015 12:04:00 PM ####
You can use the following formula to download both a package-management-client tool (paket.exe) at the start of a script and then use it to then download nuget packages:
https://gist.github.com/dsyme/9b18608b78dccf92ba33
It's really cool and close to what's needed, without building in things into F# Interactive.
Adding #nuget to F# Interactive would be a smoother experience, but also has some risks (e.g. nuget is still an evolving thing in many ways).


#### Comment by exercitus vir on 6/19/2015 5:54:00 PM ####
I like that this would be independent of the package management client.


#### Comment by zjv on 12/4/2015 7:18:00 AM ####
It would be nice if one could also easily import DLL's from projects in the current solution !


#### Comment by Jared Hester on 6/28/2016 12:38:00 AM ####
Instead of a specific directive what if we could define a set of preprocessors with custom behaviors in a dll and have fsi automatically reference that assembly at startup.


#### Comment by Gauthier Segay on 7/28/2016 7:11:00 PM ####
issue on github https://github.com/Microsoft/visualfsharp/issues/56

