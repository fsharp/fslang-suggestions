# Add ofObj to Seq and Array [16092382] #

**Submitted by Mark Seemann on 9/15/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

The Option module defines Option.ofObj which converts a potential nullable value to an option.
Collections (Seq and array) can be null in interop scenarios, but it'd often be natural to interpret a null collection as an empty collection.
It's possible to compose such behaviour from existing building blocks, e.g. with Option.ofObj >> Option.toArray >> Array.concat
This seems like quite a roundabout way to do things, so I'd like to propose equivalent functions for Seq and Array:
// seq<'a> -> seq<'a>
Seq.ofObj
// 'a [] -> 'a []
Array.ofObj



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/16092382)**


## Comments ##


#### Comment by Loic Denuziere on 9/16/2016 8:10:00 AM ####
Alternatively for something more general, we could have a null equivalent of `defaultArg`. So if it's called let's say `ifNull` (placeholder name, not actual proposal) then your `Seq.ofObj s` would be `ifNull s Seq.empty`, and `Array.ofObj s` would be `ifNull s [||]`.

