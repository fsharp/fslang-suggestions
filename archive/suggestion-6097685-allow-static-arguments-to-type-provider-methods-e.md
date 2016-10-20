# Allow static arguments to Type Provider methods eg M<"ABC">() [6097685] #

**Submitted by Dmitry Morozov on 6/25/2014 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

This in addition to static arguments to types.
Use case:
http://fsprojects.github.io/FSharp.Data.SqlClient/
SqlCommandProvider typical usage is
type MyCommand1 = SqlCommandProvider<"SELECT 42", connStr>
type MyCommand2 = SqlCommandProvider<"SELECT 43", connStr>
Some information as connection string and database-level info (user defined types for exaample) can be shared. Only query itself is different. It will look like:
type MyDb = SqlCommandProvider<connStr>
type MyCommand1 = MyDb.GetCommand<"SELECT 42">
type MyCommand2 = MyDb.GetCommand<"SELECT 43">
Shared db definition will bring performance benefits to this particular provider. Sharing types (especially user defined table types used for table-valued parameters) will allow to pipe output of one command into input param of another.
This change will enable to merge SqlCommandProvider and SqlProgrammability into single cohesive type provider
type AdventureWorks = SqlClient<connStr>
Triggered by dsyme tweet
https://twitter.com/dsyme/status/430094038771843072



## Response ##
** by fslang-admin on 11/12/2014 12:00:00 AM **

This is now completed and available in preview releases of F# 4.0.
For an early Visual Studio preview release see here (cross platform releases will follow) – http://blogs.msdn.com/b/fsharpteam/archive/2014/11/12/announcing-a-preview-of-f-4-0-and-the-visual-f-tools-in-vs-2015.aspx
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6097685)**


## Comments ##


#### Comment by Don Syme on 7/29/2014 1:13:00 PM ####
An early prototype (including a pull request and a sample using it) is detailed at: https://github.com/dsyme/SampleMethStaticParamProvider/blob/master/README.md

