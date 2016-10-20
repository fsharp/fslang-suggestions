# create a standard free open source comprehensive machine learning library [5710458] #

**Submitted by Steven Sagaert on 4/1/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Like suggested on the F#.org website, F# could be an excellent language for modern machine learning. In fact it could be one of it's killer niches. There a few C# ML libs like Accord.net that one can call from F# but there isn't a "native" F# one using those wonderful F# specific features (e.g. type providers, async & parallel,...) and exposing a functional API.
Rather than hoping that such a library will spontaneously emerge from the open source community maybe a more structured approach should be followed and the initiative should be taken by the core team responsible for the F# platform (of course volunteers from the ML community should be able to join in and collaborate). This would ensure one large comprehensive ML library with a uniform style covering all of the modern ML models (kernel models,Bayesian models/probabilistic graphical models, deep learning, ensemble methods,...) rather than N little open source libraries each which implement a small fraction of the models and each in another style/API.
Since this is 2014 and the multicore & cloud revolution is now firmly upon us, this library should aim to implement as much a possible data parallel versions of the algo's (if possible of course) and also distributed versions to run on clusters/cloud because that's what's missing from most ML libs out there (in any language).



## Response ##
** by fslang-admin on 6/25/2014 12:00:00 AM **

See comment and links by Don Syme.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5710458)**


## Comments ##


#### Comment by Don Syme on 6/25/2014 7:10:00 AM ####
Hi Steven,
I'm strongly sympathetic to this and consider it really important for growing F# use in this area.
This is a bit off topic for fslang.uservoice.com, which is about the F# language and core library (FSharp.Core), so I'll decline it here. However some upstack open source efforts to get involved in would be
- http://fslab.org
- MathNet.Numerics
- other machine learning packages and projects on http://nuget.org
- make Vorpal Wabbit better available for C# and F# and document its use http://hunch.net/~vw/
- likewise with other industry-standard machine-learning libraries
Anything you do or get involved with can be documented at http://fsharp.org/guides/machine-learning/
Thanks
Don

