# Add more persistent collections [7089800] #

**Submitted by Nils Lück on 2/13/2015 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Immutability is one of the large advantages of functional programming. However, in order to effectively utilize such immutability, a good set of persistent data structures are necessary.
Other modern functional programming languages like Scala and Clojure offer a much richer set of immutable data structures, which makes F# feel lacking in this respect, and this in turn encourages developers to fall back to regular .NET collections.
Whereas third party alternatives exist, common data structures are so general, that they should be in the std. library. We should at least add the following:
- persistent queue
- persistent vector
But we could consider adding more efficient HAMT based maps/sets, and immutable arrays, as well



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as completed – evolution will be done through additional packages like those mentioned, and there are already several good packages available.
For discussion see the comments below. Further discussion and links to newly available libraries welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7089800)**


## Comments ##


#### Comment by Don Syme on 2/13/2015 4:11:00 AM ####
Use System.Collections.Immutable? https://msdn.microsoft.com/en-us/library/dn385366(v=vs.110).aspx


#### Comment by Nils Lück on 2/13/2015 1:28:00 PM ####
Then we should at least provide a nice wrapper api for those - working with the C# api is cumbersome at best. Also, it doesn't seem overly consistent with the custom map/set implementation we have now.
Further, their chosen data structures are inferior at best. A Bitmapped vector trie is much faster than an AVL tree vector. And the current queue implementation was not persistent the last time I looked in the source.
One of the key advantages of a language like clojure is that it provided a rich set of efficient immutable and persistent data structures, all with a nice and consistent API. This makes working with immutable data a joy. One of the reasons, I assume, they spend much energy on that part.


#### Comment by Don Syme on 2/14/2015 11:16:00 AM ####
Nils - have you checked out FSharpx.Collections? That may be a good place to contribute top-quality immutable data structure implementations. ExtCore is another possibility.
However I agree it would be good to bring the best of these streams together into an FSharp.Collections.Immutable


#### Comment by Don Syme on 6/9/2015 2:16:00 PM ####
All in all I think this belongs outside FSharp.Core. I am very supportive of better immutable collections (and we actually have a fabulous set of collections in System.Collections.Immutable -= which are actually very nice to use from F#).
But I think any F# view of these (or additions to them) is best developed as an add-on package.


#### Comment by Don Syme on 7/17/2015 8:21:00 AM ####
As mentioned below, there are many good options for additional immutable collections with F# - some of the options are listed below.
The recommendation is that any additional new immutable collections should be added to F# community libraries (with nuget packages) or as new standalone nuget packages. Listing the packages on http://fsharp.org and putting their implementation in http://github.com/fsprojects is a good option.

