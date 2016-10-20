# Fix the #use directive in F# interactive [5670098] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

F# interactive supports a --use:myfile.fsx flag on the command-line, which pulls in the code from the myfile.fsx script just as if you manually typed the file's contents into the REPL. This is subtly -- but critically -- different from the --load:myfile.fsx flag, which compiles the code and imports it into the current REPL environment.
Within the F# interactive shell, you can issue #load "myfile.fsx" directives to perform the equivalent of specifying --load:myfile.fsx on the command line. There is currently no equivalent #use "myfile.fsx" directive equivalent to the --use:myfile.fsx command-line flag; looking through the F# source code, it appears this was attempted at some point and abandoned. I tried to finish the implementation when working on the NHol project (a port of hol-lite to F#), but ran into some issues I was unable to resolve. I'd be happy to share the work I did if it would be helpful in getting the #use directive implemented.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Declining as the removal of #use was indeed deliberate – the need to parse and import all directives from used files made source analysis of scripts in the editor considerably more difficult than we liked.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670098)**


## Comments ##

