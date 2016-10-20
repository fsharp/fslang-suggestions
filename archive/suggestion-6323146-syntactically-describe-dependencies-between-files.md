# Syntactically describe dependencies between files (by using '#requires', '#load' or extending 'open' syntax) [6323146] #

**Submitted by Daniel Bradley on 8/20/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

With F# becoming more and more multi-editor and cross-platform, it is becoming increasingly difficult to teach all build/edit tools about F#'s file order. The F# community are currently struggling to "update" each new build/edit tool to understand that F# actually needs a file order.
Part of the problem is that there is no standard textual way to specify this file order except as command line arguments, and these are not stored in an editable form. There is no standard way to specify the F# file order. We need an (optional) solution to this problem that is closer to home and doesn't involve modifying build/edit tools.
This proposal is one of three alternatives to deal with this problem in the F# language/compiler itself.
The specific proposal covered by this UV entry is to use #requrie declarations within files to specify a file order
#require "Helpers.fs"
Then, the compiler could automatically infer the dependencies between the files and not require files to be passed in pre-ordered by least dependent first.
Related alternative #3: Keep a file order, but optionally have it specified by a fileorder.fsx or fileorder.txt or fileorder.json: /archive/suggestion-13394442-optionally-specify-file-order-by-a-fileorder-fsx



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6323146)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 2:49:00 PM ####
Other suggestions have been
#requires "Helpers.fs"
or
#load "Helpers.fs" (which already describes dependencies in scripts)
See also /archive/suggestion-6323146-describe-dependencies-between-files-by-extending


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 2/3/2016 2:51:00 PM ####
See /archive/suggestion-10276974-allow-the-compiler-to-take-source-code-files-in-an


#### Comment by Don Syme on 2/5/2016 5:29:00 AM ####
Closing this in favour of /archive/suggestion-10276974-allow-the-compiler-to-take-source-code-files-in-an

