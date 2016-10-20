# Add (binary) search function to Map and Set [13133787] #

**Submitted by Anthony Lloyd on 3/25/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Often in interpolation the nearest collection items to a given value are needed. Map and Set both have a data structure that could be binary searched returning the two nearest neighbours optionally. The function should only be called something like 'nearest' so the implementation isn't exposed.
At the moment you would have to replicate the collections to be able to do this.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13133787)**


## Comments ##


#### Comment by Jon Harrop on 3/28/2016 6:00:00 PM ####
Implementing "nearest" will require the concept of distance, above and beyond a mere total ordering. OCaml provides a Set.split function that splits a set into two sets at the given element, returning a boolean if that element was present.
I wish there were many more functions in Map and Set. I'd like a subset function for Map where you give it a Set of keys. And a merge function for Map that adds binding from one Map to another efficiently (can be done in sub-linear time with pure collections). FWIW, my preference would be for more jack-of-all-trades-and-master-of-none purely functional collections. Their performance inevitably sucks so their value is really ease of use and clarity.


#### Comment by Anthony Lloyd on 3/29/2016 3:23:00 AM ####
It would only need comparison on the key which it already has. I'm thinking of a function a little like Array.BinarySearch. It should probably be called something like search unless that conflicts with some other use.
A more generic iter or fold function could be a possibility if it would be useful for exposing other functionality based on the fact that the structure is a tree.

