# Compiler Plugins like Rust [9451143] #

**Submitted by Jared Hester on 8/23/2015 12:00:00 AM**  
**59 votes on UserVoice prior to migration**  

In Rust compiler plugins are user created libraries that can extend syntax behavior with new syntax extensions, lint checks, etc.
A compiler plugin system would enable a laboratory of experimentation with language features, giving them the potential to prove themselves trough implementation and application. There are definitely some language features that people have requested that may not seem like a worthwhile investment of resources due to their lack of relevance to a broad spectrum of users, but a compiler plugin system could remove that roadblock from their path toward reification.
A compiler plugin system facilitates a marketplace of ideas. The interchange of approaches, goals, pitfalls and adaptations will distill the best augmentations to the point where they might even be worthy of being incorporated as a part of the core language.
http://smallcultfollowing.com/rust-int-variations/imem-umem/guide-plugin.html



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declining per my comment below: right now this is best registered as an FSharp.Cpmpiler.Service feature request.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9451143)**


## Comments ##


#### Comment by Bryan Edds on 8/23/2015 8:23:00 AM ####
Yes, one reason Haskell is so 'inexplicably' popular is because that language is so hackable. Anyone with sufficient need can extend the language in way unanticipatable by its original designers.
While a market place for language ideas may seem chaotic at first, it draws a surprising level of participation and cooperation. Like how boost was just a library that ended up helping C++ evolve in fundamental ways, F# plugins will eventually be tremendously beneficial in guiding the future of F#, and in a principled way.
This could also hold off a non-cooperative fork of which I keep hearing murmurs :) It appears to be time to open this pressure valve in the community, I think.


#### Comment by Don Syme on 2/4/2016 12:43:00 PM ####
This is best registered as an FSharp.Compiler.Service request.
There is no current plan to have the fsc.exe compiler shipped as part of the Visual F# Tools or the fsharpc compiler shipped on Mono accept plugins. However using FSC it is possible to create a new binary that does compilation and accepts plugins.

