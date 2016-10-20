# Add atom syntax [8556646] #

**Submitted by mikero on 6/26/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Add a syntax for atoms a.k.a. keywords a.k.a. self-evaluating symbols.
:foo (or 'foo, or #foo - whichever causes the least problems)
Where foo otherwise follows the rules for an identifier, is simply turned into "foo" at compile time. (It would also be nice of '-' were also added to the list of allowable characters for the atom.)
E.g.:
("fido", :is-a, :pet) is of type string*string*string



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8556646)**


## Comments ##


#### Comment by Shawn Hoover on 10/30/2015 2:10:00 PM ####
Is there a particular reason why self-evaluating symbols don't exist in a lot of statically typed languages? I've been wondering about it since hearing Rich Hickey stress in some talks the idea of using generic data (maps, vectors, lists) at subsystem boundaries. Obviously they've been around a long time in Lisp, Erlang, and Ruby, for example. Is it just that generic maps are used less in F# so whatever efficiency or syntactic gains of keywords is less useful?
I see someone bothered to make a library in Haskell: https://hackage.haskell.org/package/hxt-9.3.1.15/docs/Data-Atom.html


#### Comment by Don Syme on 2/4/2016 5:31:00 PM ####
Why wouldn't it have some new type "Atom" (e.g. a single field struct wrapping a string)


#### Comment by mikero on 2/4/2016 6:36:00 PM ####
>Why wouldn't it have some new type "Atom" (e.g. a single field struct wrapping a string)
That's fine too -- I was just trying to create the least amount of friction possible and make the Atom an erased type.
They should always be interned strings so that they are object.== with an atom or a string with the same chars w/o doing a strcmp. (Wouldn't the wrapping interfere with this?)
Ah, the atom could be a global object in the assembly so, :foo would be

namespace __atoms {
static readonly string __gsym_foo = "foo";
}
or, per your comment:
static readonly string __gsym_foo = new Atom("foo");
So we could get pretty-print the right way, or store properties on the atom or whatever.
So the compiler turns :foo into __atoms.__gsym_foo, and :foo == :foo is always true, at least in the same assembly. (Although getting the symbol from a dynamic string (which is not the normal use case) still requires a lookup.)
If we had symbols and a lightweight first-class map syntax (please!) then I'd be at least 34.7% happier:
let map = #{:foo 1 :bar 2; :baz 3} --> map<string,int> or map<Atom,int>
match map with #{:foo 1 :bar n :REST more} -> /* n =2, more=[ (:baz,3) ] */
(Of course, reader macros would let us do these things ourselves :) and make me 99 44/100 percent happier. Even w/o homoiconicity, I'd deal that the AST transforms to get macros and reader macros - but I know it's a bit of a sticky wicket as well.)
I'm using Clojure over F# for a current project now for some of these reasons, even though I'd much prefer to stay in the .Net ecosystem, and F# in particular -- I'll end up having to do loosely-coupled Java/.Net interop.
Another option (or related one) is to improve F#'s default use of "?" dynamic access, so that out of the box it does all the fast expando object / call-site caching stuff, etc., but still let it be overridable.
It seems to be that record/class syntax and map syntax and pattern matching could be merged, so that the same pattern could match any complete or partial sum type, and that this would afford a way to do a sort of "gradual typing" in F#. Basically I could use record syntax that was a *partial* specification of the record - the backing store would be a map, not a class, and then the type could "graduate" to a fully-specified type at some point backed as a class/struct. Devil is in the details...

