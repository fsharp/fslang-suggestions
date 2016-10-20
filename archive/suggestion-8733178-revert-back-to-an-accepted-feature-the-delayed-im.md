# Revert back to an accepted feature the delayed implementation of interfaces [8733178] #

**Submitted by Enrique A. Casanovas Pedre on 7/6/2015 12:00:00 AM**  
**24 votes on UserVoice prior to migration**  

Please see:
http://stackoverflow.com/questions/31248797/delay-the-implementation-of-interface-methods
Allow this as a normal, valid and completly legal code:
type MyCollection<'T> =
{ Data : 'T list }
interface IEnumerable<'T>
interface IEnumerable
let getEnumerator { Data = d } =
(d :> seq<_>).GetEnumerator()
type MyCollection<'T> with
interface IEnumerable<'T> with
member this.GetEnumerator() = getEnumerator this
interface IEnumerable with
member this.GetEnumerator() = (getEnumerator this) :> _
Currently the compiler says:
Interface implementations in augmentations are now deprecated. Interface implementations should be given on the initial declaration of a type.
This style allows for a more idiomatic and functional approach of developing in F#.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Many thanks for the suggestion. I’m closing it per my comment below, and in favour of this suggestion: /archive/suggestion-11723964-allow-types-and-modules-to-be-mutually-referential
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8733178)**


## Comments ##


#### Comment by Tomas Petricek on 7/6/2015 9:47:00 PM ####
I also prefer to define types in this way (core type definition, followed by a module with functions, followed by an augmentation that exposes the functionality in an OO friendly way), so I support the suggestion. Especially since it's pretty much just a matter of removing a warning :-)


#### Comment by Don Syme on 7/17/2015 6:06:00 AM ####
The technical reason that this is deprecated is that initialization may be unsound, e.g. https://gist.github.com/dsyme/d02446c3e139a7b81f28.
The F# approach to this would be to add dynamic initialization checks to initialization sequence in cases where this construct is used and there is intervening top-level data (e.g. see http://research.microsoft.com/apps/pubs/default.aspx?id=79951)
This is in theory feasible - similar checks are done for static data initialization in classes and it would be great to share the implementation - but it is non-trivial to implement and comes with a runtime cost which must be avoided for all existing code. Also, there have historically been a lot of niggling issues with that particular feature.
So in short this is feasible, but is not simply a matter of turning the deprecated feature back on.


#### Comment by Don Syme on 2/4/2016 4:53:00 PM ####
I'm closing this per my comment below, and in favour of this suggestion: /archive/suggestion-11723964-allow-types-and-modules-to-be-mutually-referential

