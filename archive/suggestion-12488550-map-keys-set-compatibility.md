# Map keys <--> set compatibility [12488550] #

**Submitted by mikero on 2/26/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

A map's key collection is a set and should be treatable as such. Currently (AFAIK) you must get the keys from the map like so:
let keys = Map.toSeq >> Seq.map fst
then create a set from the (k,v) seq:
let set1 = keys map1 |> Set.ofSeq
and then perform your set operation:
let common = Set.intersect set1 set2
This involves creating a temporary collection and a new set.
There are several ways to improve things:
(1) Provide a Map.toKeySet & Set.ofMapKeys functions that will directly and efficiently create a new set from the Map's keys. This is straightforward and should be done, but will create a new set, which may not always be warranted.
(2) Provide a functions that treat the Map's key as a set, exposing some/all of the set operations - at least intersect/difference.
For example: Map.keySetIntersect & Map.keysetDifference, or using a nested name Map.keySet.intersect, etc.
(3) Provide set-like functions that work on Maps and produce new Maps. Map.difference and Map.intersect. (Note map intersect would be Map<k,v> -> Map<k,v> -> Map<k,v*v> )
Each of these has it's own use case.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12488550)**


## Comments ##

