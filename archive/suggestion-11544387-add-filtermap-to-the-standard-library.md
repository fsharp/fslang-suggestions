# Add filtermap to the standard library [11544387] #

**Submitted by Dave Thomas on 1/22/2016 12:00:00 AM**  
**23 votes on UserVoice prior to migration**  

Add filtermap to the standard library
Rust, Elixir and other functional languages have this and it would be nice to have an alternative to the option allocating choose function:
let filtermap (filter:a->bool) (map: a->b) (xs: a list) -> b list = ...
Elixir:http://elixir-lang.org/docs/v1.0/elixir/Enum.html#filter_map/3
Rust: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter_map



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per my comment below
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11544387)**


## Comments ##


#### Comment by NhlCrd on 1/25/2016 2:45:00 AM ####
Isn't it a one-liner in F#?
let inline List.filterMap f m l = List.filter f >> List.map m


#### Comment by Dave Thomas on 1/25/2016 4:04:00 AM ####
You can compose a one liner but that would iterate over elements in the list twice. A standard library function would be optimised.


#### Comment by Phil de Joux on 1/25/2016 8:11:00 AM ####
Elm's got it too ...
http://package.elm-lang.org/packages/elm-lang/core/1.0.0/List#filterMap


#### Comment by Daniel Robinson on 1/25/2016 9:46:00 AM ####
Isn't this equivalent to Seq.choose?


#### Comment by NhlCrd on 1/26/2016 2:53:00 AM ####
@Dave Thomas
Right. Do you know if that would happen with the lazy Seq module as well? In C#/VB, a concatenated LINQ expression like .Where().Select() would be compiled into a single loop, I believe.


#### Comment by Don Syme on 2/4/2016 3:53:00 PM ####
My problem with this suggestion is that there are many, many other combinations of pairs or triples of functions which could be optimized (fused). Adding just one seems incorrect. Why not filterCollect? filterSum? filterMax? filterMin? filterGroupBy?
I am going to decline this on this basis.


#### Comment by Dave Thomas on 2/6/2016 5:02:00 PM ####
Thats a shame, I have never had need of the other function combination you mentioned but filter-map is something that I use quite often, an alternative would be to optimise Choose so the option allocation goes away.


#### Comment by Dzmitry Lahoda on 2/9/2016 7:09:00 AM ####
Seems BCL LINQ optimizes such case http://referencesource.microsoft.com/#System.Core/System/Linq/Enumerable.cs,3df3a8bfcaaa2b6d,references
```
if (predicate == null || predicate(item)) {
current = selector(item);
return true;
}
```


#### Comment by Dzmitry Lahoda on 2/9/2016 7:27:00 AM ####
As I know implementation of LINQ (both IEnumerable and IQueryable) are based on direct casts like next:
```
if (source is Iterator<TSource>) return ((Iterator<TSource>)source).Where(predicate);
if (source is TSource[]) return new WhereArrayIterator<TSource>((TSource[])source, predicate);
if (source is List<TSource>) return new WhereListIterator<TSource>((List<TSource>)source, predicate);
```
E.g. some ORM would have own collection and cast on them.
Not sure, but may be in Scala(Dotty) there is way to achieve such optimizations without coding all casts directly. I.e. compiler somehow identifies concrete types/methods to use and uses more faster methods and reduce casing and intermidiate collections. So that when I implement my collection it can be plugged into collection framework in optimized way without changing collection framework code.
So if this is case and F# has not such - may be this could be proposal.
http://stackoverflow.com/a/1728140/173073

