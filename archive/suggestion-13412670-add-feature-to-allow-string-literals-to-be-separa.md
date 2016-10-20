# Add feature to allow string literals to be separated into text files [13412670] #

**Submitted by Jeffrey Pierson on 4/13/2016 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

Often in code there is a block of meta language in a string format. Typical examples could be SQL, XML, JSON, MD, or just plain text. The choices a developer normally has is either to embed the text as a string literal or to spearate into a file. Separating into a file normally has some advantages in that the format gets better editing support (ex. MyQuery.sql has a nice editing experience than an embedded string) and it cleans up the related code. The down side is traditionally that now the file is read in at runtime and the tooling support in the code to go to the text file for a given string definition becomes more of a manual process.
What I would like to propose is the idea of a string literal where the value can be specified in a referenced text file.
Before:
_program.fs_
let myQuery = "select a, b, c from mytable"
After:
_program.fs_
let myQuery = @mytable_query.sql
_mytable_query.sql_
select a, b, c
from mytable



## Response ##
** by fslang-admin on 6/13/2016 12:00:00 AM **

Having a type provider to read string literals from files is entirely reasonable.
I am marking this as declined for the F# language itself because the functionality can be implemented using F# type providers. My suggestion is to open an issue at https://github.com/fsprojects/FSharp.Management/issues
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13412670)**


## Comments ##


#### Comment by Radek Micek on 4/16/2016 9:05:00 AM ####
You can do that with type providers.


#### Comment by Jeffrey Pierson on 4/27/2016 12:29:00 PM ####
Radek Micek - care to share how? I haven't found any available type provider for string literals and looking into how to create a custom type provider has led me into what seems to be a deep rabbit hole.


#### Comment by Don Syme on 6/13/2016 5:20:00 AM ####
This is possible with F# type providers, but the functionality needs to be implemented. I tweeted a request for someone to help with this here: https://twitter.com/dsyme/status/742300239739166720


#### Comment by Gauthier Segay on 6/21/2016 8:39:00 AM ####
Jeffrey Pierson, please look at this type provider I created to read a .csv file, parse values from a single column, and generate distinct string literals from those:
https://gist.github.com/smoothdeveloper/94332dbd7b894d2dc45cbc1f47a75ac5
I think your feature request is "as simple as you could get" exercise to write your first type provider :)

