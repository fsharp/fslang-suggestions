# replace COM PdbWriter with F# PdbWriter [6153074] #

**Submitted by Cameron Taggart on 7/9/2014 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

Please replace the COM based PdbWriter and with a fully managed F# PdbWriter that can be used on Mono on Linux too. As adoption of F# increases on Linux, it is important that debugging binaries be able to be shared. Source indexing leverages pdb files and this would be great to have on Linux as well.
I wrote SourceLink which is an F# project with an Apache License. It is able to read the Root and Info streams of a pdb. It could be used as a starting point. I was hoping to be able to reverse engineer the entire pdb file, but it is a fairly difficult task without access to some of the legacy source code or Microsoft engineering support.
https://github.com/fsharp/FSharp.Compiler.Service/blob/master/src/absil/ilsupp.fs#L867
https://github.com/ctaggart/SourceLink



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per comment by Don Syme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6153074)**


## Comments ##


#### Comment by Don Syme on 9/3/2014 4:58:00 AM ####
Hi Cameron,
That would be great - but do you know of an appropriately licensed and available F# PDB writer?


#### Comment by Don Syme on 9/3/2014 4:58:00 AM ####
(Or even a spec for the PDB format)


#### Comment by Don Syme on 2/3/2016 2:41:00 PM ####
Appropriate changes to PDB/MDB/... writing are happening as part of the CoreCLR work. I'll close this as while we will continue to use the COM PDB writer, other writers will be in managed code AFAIK

