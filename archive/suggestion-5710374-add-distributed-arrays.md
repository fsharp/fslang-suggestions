# add distributed arrays [5710374] #

**Submitted by Steven Sagaert on 4/1/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Like suggested on the F#.org website, F# could be an excellent language for modern scientific computing/machine learning. However for large scale computing (Big Data), it is missing some things. One of these is distributed (in-memory) arrays. I was hoping that "Microsoft Cloud numerics" would have been available by now but like so many MSR projects this one seems to have died a quiet death. So I propose to add a distributed array type directly to F# similar to Fortran co-arrays (see co-array Fortran of Fortran 2008). This could be implemented on top of MPI (MS MPI, MPI.NET). That would make it run from a single host, a cluster of servers connected via ethernet to a real supercomputer with a grid-type network.
This would allow to build parallel & distributed algo's to run on computed clusters/cloud for number crunching & large scale machine learning ("big learning" on big data).



## Response ##
** by fslang-admin on 6/25/2014 12:00:00 AM **

Declined, see comment by Don Syme,
“As with /archive/suggestion-5710458-create-a-standard-free-open-source-comprehensive-m, I’m very sympathetic to this request. An upstack library in this domain would be a great addition to the F# ecosystem, and its possible some upstack .NET libraries already exist for this, or other R/Python libraries that can be used from F#.
Right now it’s off topic for fslang.uservoice.com, which focuses on the language and core library FSharp.Core.
Have you searched around for F#, C# open source projects implementing distributed arrays for .NET, publishing packages on http://nuget.org, or considered starting one?
"


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5710374)**


## Comments ##


#### Comment by Don Syme on 6/25/2014 7:16:00 AM ####
Hi Steven
As with /archive/suggestion-5710458-create-a-standard-free-open-source-comprehensive-m, I'm very sympatheric to this request. An upstack library in this domain would be a great addition to th F# ecosystem, and its possible some upstack .NET libraries already exist for this, or other R/Python libraries that can be used from F#.
Right now it's a bit off topic for fslang.uservoice.com, which focuses on the language and core library FSharp.Core.
Have you searched around for F#, C# open source projects implementing distributed arrays for .NET, publishing packages on http://nuget.org, or considered starting one?
This would be a great addition to the

