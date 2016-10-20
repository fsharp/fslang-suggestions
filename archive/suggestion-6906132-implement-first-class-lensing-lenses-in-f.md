# Implement first-class lensing / lenses in F# [6906132] #

**Submitted by Bryan Edds on 12/31/2014 12:00:00 AM**  
**168 votes on UserVoice prior to migration**  

When working with complex state structures, functional programming is, without a great deal of additional tooling (tooling that does not satisfactorily exist in F#), highly inconvenient, verbose, and even error-prone. These problems are so pronounced that many cite them as a reason to label functional programming itself as inapplicable to the domains within which complex state structures are inherent!
As functional programmers, we believe otherwise, and many even believe that it is in the domain of dealing with complex state artifacts that functional programming is especially beneficial and necessary! However, with such weak syntactic constructs such as these -
let a = { a with B = { a.B with C = c }}}
- we win ourselves no favors.
And even in the narrow context of such a small problem, simple and promising solutions abound. For example, why doesn't this syntax have a semantics assigned to it in F#? -
let a = { a with B.C = c }
Or better, given that we know at compile-time that there is a means of constructing A and B, why we can't assign a semantics to this -
let a = a.B.C $= c
- and generate all the backing code for such a pure functional update automatically?
And why restrict such nice syntax to only record fields? Why not let it be applicable to all members who support the concept of readability and updatability (EG - lensability) such as with here -
type Entity with

member gui.Enabled = gui?Enabled : bool
static member setEnabled (value : bool) (gui : Entity) = gui?Enabled <- value
so that we can finally utter -
let entity = entity.Enabled $= anotherEntity.Enabled
In other words, why not give the compiler some way of recognizing 'lensability' implicitly for simple cases (and perhaps explicitly with simple declarations in more refined cases such as with Map values), ultimately enabling good syntax to take advantage of it all?
And yes, there have been library solutions to the problem of lensing proposed in F#. However, in experience I have found the library solution to be embarrassingly inadequate. This is due to the fact that F# does not provide out-of-the-box (nor shall it in the reasonably near-future) the language constructs necessary to build a sufficiently expressive lens library... and not even for the straight-forward use cases I outlined above! And, even if such language constructs were available, I still doubt that a form of expression as understandable and succinct as the syntax I proposed could be achieved.
For that reason, I did and still do conclude that it is necessary to build lensing as a first class construct in the language. This is so that instead of attempting to use kindedness to express lensing, the simpler (and admittedly more muscled) approaches of syntactic expansion / IL generation may be used. Thus this user suggestion.
(On a side note, perhaps if we had a sophisticated and general syntactic macro system in F# like I suggested here - /archive/suggestion-5674940-implement-syntactic-macros, the solution could again be proposed as a library. However, given that such a feature whose design and implementation is daunting and not yet to be even approved in principle, this too is a non-starter for an urgently-needed construct.)
To expand on the design proposal further, et's look at the subtle distinction I've made in the words I've used above. Specifically, we notice a distinction between -
Lensing - viewing or updating a value contained by another functional value
Lenses - a general mechanism by which lensing is achieved
We've already seen the syntax I propose for lensing where the lens itself is contextually implied -
let a = a.B.C $= c // here a new value of a is constructed and bound to a shadowing binding of a.
Now say we want to pull out the lens itself that it might be passed around for lensing later. Obviously, we will need a syntax for that as well. However, the desired form taken by that syntax is more nebulous, so here are a few options -
let abcLens = lens <@ A.B.C @> // here's a syntax that utilizes code quotations: verbose but maybe easier to implement in the compiler?
let abcLens = lensOf A.B.C OR lensOf<A.B.C> // here's lens with a new keyword lensOf: succinct, but not perfect backward compatibility
let abcLens = {$ A.B.C $} // ugly, but succinct and probably backward compatible (but maybe not as I've yet to study F#'s AST in-depth).
...and there are presumably many more possible forms. After all, for literally ALL the syntax I've proposed in this thread, I've merely been riffing!
Additionally, there would need to be a syntax for allowing user-defined induction of other things into the category of 'lensability'.
For example, say we have a type whose members are described at run-time like so -
type A with

static member getB (a : A) = a?B : bool
static member setB (b : bool) (a : A) = a?B <- value
We should be able to decorate the view and update functions like so -
type A with

[<Viewable "B">] static member getB (a : A) = a?B : bool
[<Updatable "B">] static member setB (b : bool) (a : A) : A = a?B <- value
In conclusion, F# needs first-class support for lensing / lenses because it current set of language features is inadequate to provide a library solution, and because lensing / lenses is such a fundamental property of functional programming in stateful systems. While my design proposal certainly will have some flaws that need to be smoothed over, I think it is a good enough start to get something in the works!



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6906132)**


## Comments ##


#### Comment by Christopher Stevenson on 1/9/2015 10:14:00 PM ####
Coming from an object-oriented background, I find it difficult to understand what lenses are, besides 'functional version of properties'. Even though this proposal is rather lengthy, I'm not really understanding what the benefit of this is, besides some vague notion of more concise field setting of copied records.
If someone could point to a good primer, I'd appreciate it.


#### Comment by Fraser Waters on 1/12/2015 11:22:00 AM ####
Functional properties is a pretty good way of putting it. The one part that Bryan didn't really cover well in this is that the lens is an instance of an object itself. So given his example of "lens <@ A.B.C @>" that would create a lense for field C of field B of type A. That lens object is a function that can either get that value from an instance of A, or set that value on an instance of A (returning a new A).
eg something like:
let l = lens <@ A.B.C @>
let a = // create some A value
let c = get l a // c is now the same as a.B.C
let newC = // create some C value
let newA = set l a newC // newA is now the same as { a with B = { a.B with C = newC } }
Lenses themselves aren't massively complex, it's pretty much just:
type Lense<a', b'> = { getter : a' -> b'; setter : a' -> b' -> a' }
let get lense obj -> lense.getter obj
let set lense obj value -> lense.setter obj value
but with that you can then add composibility and other nice functional things on top. The awkard bit of lenses is constructing those getter/setter functions (more so the setter), but the construction of those functions is also trivial to the compiler.


#### Comment by Anonymous on 1/19/2015 11:27:00 AM ####
I think it is critical to look at the different versions of this concept and how they evolved in Haskell -- my understanding, weak as it may be, is that it took a while to get to ekmett's package and that is the one that you would want to model it after.
One key thing that you want to preserve would be in addition to a regular getters and setters, you want the ability to set a value with function that uses the original value. For example, if you have a property that is an integer, you should be able to set it with an incrementing function:
f x = x + 1
and all of the variations that you might want with that.


#### Comment by Bryan Edds on 1/19/2015 11:48:00 AM ####
I think those are just a matter of defining the right operators.
I think also there is a marked difference in the scope of what Haskell's lenses accomplishes and what we actually need in F#. The two may differ more than one may initially think. Or not - I too am no expert.
However, I think it would be great to ask Edward Kmett himself to take a look at the lens proposal during the design process. Though he is busy as always, and even though he's not an F# user AFAIK, I think he would willing to prioritize some time for it.
I have his contacts, and he spends a good deal of time on #Haskell on Freenode IRC.


#### Comment by Andrew Cherry on 2/13/2015 6:19:00 AM ####
I think I commented a bit on this elsewhere in a discussion, but it came up again just now in another context ( https://github.com/SuaveIO/suave/pull/206#discussion_r24602874 ), and @dsyme thought it might be useful to include here...
I use lenses (Aether library), but they're not the Kmett library style of lens (which, from memory, are van Laarhoven lenses). With our type system as it stands, we're restricted to the more naive style of lens that Aether implements (get, set pairs). I do still find that they're useful however.
(See that linked discussion for a little more detail and some examples).
However... I'm not sure I can agree with lenses, as a concept, becoming a language feature. It's overly specific, to my mind. Either we need to be saying something like
"We need a better way of modifying properties in deeply nested immutable data structures", which would be reasonable perhaps, or we should be saying "we need the type system to be a bit different/more to enable us to write some functional techniques which would make, e.g. lenses, possible". I'm not sure that lenses as a thing though is a language level change.


#### Comment by Don Syme on 2/14/2015 11:47:00 AM ####
On the specific question of "{ a with B.C = d }"... One possibility would be to give a semantics to this as follows:
{ a with ...; b.c = d } --> { a with b = { a.b with c = d}; ...}
In addition, we could also allow "setting" properties which are not record-defined properties, e.g.
{ a with ...; b = c } --> { a with ... }._set_b(c)
With these two rules we would have:
{ a with b.g = c; d = e } --> a._set_b(a.b._set_g(c))._set_d(e)
where "a" can be any kind of object as long as it has _set_b and _set_b "functional property setters". The naming _set_b could be discussed.
This is a fairly simple language feature which could be of some help, and would also address the "use record 'with' syntax on non-record types" request (/archive/suggestion-6420709-allow-record-like-obj-with-newvals-syntax-for)


#### Comment by Bryan Edds on 2/14/2015 11:46:00 PM ####
Hi Don!
I somewhat regret suggesting lensing semantics for -
let a = { a with B.C = c }
This is because B is currently used to specify the containing type of C.
Instead, I really do think we want a semantics for this more unique syntax -
let a = a.B.C $= c
Why overload existing syntax if we don't have to?


#### Comment by Jack Fox on 8/2/2015 7:27:00 PM ####
The Microsoft team has published their short-term roadmap https://github.com/Microsoft/visualfsharp/issues/563 and the long-term roadmap is coming. There are limited resources and they are deploying them wisely. What the community can do on the side is improve the documentation and publicize existing projects like http://fsprojects.github.io/FSharpx.Extras/ where lens support (among other overlooked gems) already exists.


#### Comment by Giacomo Stelluti Scala on 8/3/2015 1:22:00 PM ####
I've voted it.
I'm wondering if one day F# will have functors like OCaml, this could be implemented as library but with a deeper and more elegant support.


#### Comment by Henrik Feldt on 8/10/2015 1:29:00 AM ####
I find this proposal overly syntax-oriented: it's supposedly needed because "lenses are such a fundamental property of functional programming in stateful systems", but you can in fact easily program in a stateless manner even when using sockets, file handles, semaphores etc.
Instead, add facilities to the language to write higher kinded types, that would enable us to write van Laarhoven (http://twanvl.nl/blog/haskell/cps-functional-references) lenses, or enable us to have an officially supported Applicative namespace, or allow us to export static signatures (or type classes and instances) from modules.
Language design should be free from muck; oriented towards creating the language as a total function of its input: code, rather than lots of small partial functions over code.


#### Comment by Andrew Cherry on 8/10/2015 6:22:00 AM ####
I don't think my opinion has changed much from commenting back in February. Aether (disclaimer, i'm the maintainer) provides a reasonable library solution (in my opinion) given the constraints of the language. Even the limited possibilities that Aether provides have proven very useful when writing other libraries and being able to work with complex structures effectively. (See for example the approach that Freya takes to providing lenses in to OWIN state to provide strongly typed, safe access to request/response properties).
A specific extension of the language to support lens functionality (and realistically people only seem to be talking about "functional properties" which in my head is a small subset of the usefulness of lenses and related techniques - lenses with prisms, transducers, etc. etc.) seems over specific and maybe a little short sighted in terms of not attacking the problem in a more interesting way.
As Henrik mentions, an extension of the type system would enable us to write a far more general and useful system as a library, rather than baking specific approaches in to a language core. I'm with Henrik on this one - I would vote for careful selection of a few key extensions to the core of the language and type system which would enable new things to be built as libraries, rather than baking things that seem useful today in to the language itself. That way lies PHP.


#### Comment by Don Syme on 2/4/2016 1:58:00 PM ####
This suggestion was also relevant (and the same idea is mentioned above)
/archive/suggestion-5663252-extended-record-with-syntax-to-work-with-nested-pr


#### Comment by Don Syme on 2/5/2016 4:08:00 AM ####
See also /archive/suggestion-6906132-implement-first-class-lensing-lenses-in-f


#### Comment by Anonymous on 4/20/2016 10:14:00 AM ####
It seems that van Laarhoven style lenses allowing polymorphic updates can be encoded in F#: http://fssnip.net/7Pk


#### Comment by Ivan J. Simongauz on 9/3/2016 5:19:00 AM ####
What about observable lenses, this is almost necessary for WPF and so on.
type
change<'t> =
| Intent
| Await
| Change of 't
type ObservableLense<'t, 'tv> = ('t -> 'tv, 't -> 'tv -> 'tv, IObservable<'tv change>)

